# AWS Policy Deep-Dive: Components, Syntax & Practice — SAA-C03

> Built specifically because the practice exam tested raw policy JSON, not just policy concepts. This covers policy anatomy once, then applies it across every major policy type the exam actually uses: IAM identity-based policies, S3 bucket policies, KMS key policies, IAM trust policies, and SCPs.

---

## 1. Universal Policy Anatomy

Every AWS JSON policy — regardless of type — is built from the same elements. Learn this once, apply it everywhere.

```json
{
  "Version": "2012-10-17",
  "Id": "OptionalPolicyId",
  "Statement": [
    {
      "Sid": "OptionalStatementId",
      "Effect": "Allow",
      "Principal": { "AWS": "arn:aws:iam::123456789012:user/Alice" },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-bucket/*",
      "Condition": {
        "IpAddress": { "aws:SourceIp": "203.0.113.0/24" }
      }
    }
  ]
}
```

| Element | Meaning | Required? |
|---|---|---|
| `Version` | Policy language version — always `"2012-10-17"` (the older `2008-10-17` exists but is legacy; use current) | Yes |
| `Id` | Optional identifier for the whole policy document | No |
| `Statement` | Array of one or more permission statements | Yes |
| `Sid` | Optional label for a single statement, must be unique **within that policy** if used | No |
| `Effect` | `Allow` or `Deny` — nothing else | Yes |
| `Principal` | **WHO** the statement applies to — only appears in **resource-based** policies (bucket policies, key policies) and trust policies. **Never appears in identity-based policies** (the principal is already implied — it's whoever the policy is attached to). | Depends on policy type |
| `Action` | **WHAT** API operations are allowed/denied, e.g. `s3:GetObject`, `dynamodb:PutItem`, or wildcards like `s3:*` | Yes |
| `NotAction` | Inverse of Action — "every action except these" — rare, used for broad-deny-with-exceptions patterns | No |
| `Resource` | **WHICH** resource(s) the statement applies to, as an ARN or ARN pattern | Yes (except some IAM actions that don't target a resource) |
| `NotResource` | Inverse of Resource | No |
| `Condition` | Extra logic — IP restriction, MFA requirement, time window, tag matching, etc. | No |

**The single most exam-relevant rule from this table**: whether `Principal` is required or forbidden depends entirely on whether the policy is **identity-based** or **resource-based**. This exact distinction caused a real error in the practice test you took (a bucket policy without a `Principal` element failed to apply) — internalize this one specifically.

---

## 2. Identity-Based vs Resource-Based Policies

| | Identity-Based | Resource-Based |
|---|---|---|
| **Attached to** | A user, group, or role | A resource directly (S3 bucket, KMS key, SQS queue, SNS topic, Lambda function, etc.) |
| **Principal element** | **Absent** — the principal is whoever the policy is attached to | **Required** — must explicitly state who is being granted/denied access |
| **Grants cross-account access alone?** | No — a role/user can only act within permissions granted to it in its own account unless something on the other side (a resource policy, or an assumed role) opens the door | Yes — can grant a *different account's* principal access without that account needing a role in your account |
| **Examples** | IAM policies, permission boundaries | S3 bucket policies, KMS key policies, SQS queue policies, SNS topic policies, Lambda resource policies, VPC endpoint policies |

**Why this distinction is everywhere on the exam**: cross-account access questions are testing whether you know resource-based policies (or a role + `AssumeRole` + trust policy) can grant access *without* the other account needing an IAM user/role provisioned by you. A very common wrong answer creates unnecessary IAM users in the wrong account instead.

---

## 3. Policy Evaluation Logic (the order that actually decides access)

When a request is evaluated, AWS combines every applicable policy (identity-based + resource-based + permission boundaries + SCPs + session policies) and resolves it as:

1. **Explicit Deny anywhere → access denied.** Full stop, no exceptions. A Deny in *any* applicable policy always wins.
2. **No explicit Deny, but an explicit Allow somewhere → access allowed.**
3. **No explicit Allow anywhere → implicit Deny (default).** IAM principals have zero access until something explicitly allows it.

**Key nuance for cross-account access specifically**: for a request to succeed across accounts, the identity-based policy in the requester's account **and** the resource-based policy in the resource's account must **both** allow it (unless the resource policy alone grants access without any identity-based policy needed, or a role is assumed). One side allowing and the other staying silent is *not* enough if the specific service requires policies on both sides.

---

## 4. IAM Identity-Based Policies (attached to Users/Groups/Roles)

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowReadWriteOnSpecificTable",
      "Effect": "Allow",
      "Action": [
        "dynamodb:GetItem",
        "dynamodb:PutItem",
        "dynamodb:Query"
      ],
      "Resource": "arn:aws:dynamodb:us-east-1:123456789012:table/Orders"
    }
  ]
}
```

**No `Principal`** — attaching this policy to a role already answers "who." Attach it via `iam:AttachRolePolicy` (managed policy) or embed it (inline policy) on the user/group/role.

**Common exam traps here:**
- `"Action": "dynamodb:*:*"` — **invalid syntax**. Service actions use `service:ActionName`, not two colons. This exact malformed pattern appeared in your practice test — always check for stray extra colons or wildcards in the wrong position.
- Duplicate `Sid` values within the same policy — some services (and the policy validator) reject this; each `Sid` must be unique within one policy document.
- Using `Resource: "*"` when a scoped ARN was clearly intended — a common "technically works but violates least privilege" distractor.
- Forgetting that `Effect: Deny` combined with a broad `Resource` can accidentally block more than intended — a Deny statement's scope matters just as much as an Allow's.

**Permission Boundaries** — a special *identity-based-like* policy that sets the **maximum** permissions an IAM user/role can ever have, regardless of what their attached policies say. A permission boundary + an attached policy = the *intersection* of the two, not the union. This is a favorite exam distinction: permission boundaries never *grant* anything; they only cap.

---

## 5. S3 Bucket Policies (Resource-Based)

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowSpecificAccountPutOnly",
      "Effect": "Allow",
      "Principal": { "AWS": "arn:aws:iam::999999999999:root" },
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::my-upload-bucket/*"
    }
  ]
}
```

**Notice the `Resource` ARN ends in `/*`** — this is critical and a very common source of real (and exam) errors. Bucket-level actions (like `s3:ListBucket`) target the bucket ARN itself (`arn:aws:s3:::my-upload-bucket`), while object-level actions (like `s3:GetObject`, `s3:PutObject`) target the bucket ARN **plus `/*`** (`arn:aws:s3:::my-upload-bucket/*`). Mixing these up is one of the most common real-world (and exam) bucket policy failures — this is very likely what caused the error in the practice-test question where a policy failed to apply.

**Principal is mandatory** on a bucket policy — since it's resource-based, AWS needs to know *who* you're granting the permission to. Omitting it is invalid.

**Common S3 policy patterns to recognize:**
- **Cross-account read access**: bucket policy with `Principal` set to another account's ARN or role ARN.
- **Force encryption on upload**: `Deny` statement with a `Condition` checking `s3:x-amz-server-side-encryption` is absent or doesn't match the required value — a Deny-based enforcement pattern, not an Allow.
- **Restrict to VPC endpoint only**: `Deny` all access unless the request's `aws:SourceVpce` condition matches your VPC endpoint ID — prevents access from outside your VPC entirely, even with valid credentials.
- **CloudFront-only access (OAC pattern)**: bucket policy `Principal` is the CloudFront service principal, with a `Condition` restricting to your specific distribution's ARN — this is what "prevents direct linking to S3 assets, only via CloudFront" looks like in policy form.
- **MFA-required delete**: `Condition` checking `aws:MultiFactorAuthPresent` is `true` for delete-type actions.

**IAM Policy vs Bucket Policy for the same bucket**: both can apply simultaneously. A user needs BOTH their IAM identity-based policy AND the bucket policy to not-deny the action (per the evaluation logic in section 3) — unless the bucket policy alone grants a *different account's* principal access, in which case that external principal doesn't need a matching identity-based policy in your account (they need one in their own account, but it targets your resource ARN).

---

## 6. KMS Key Policies (Resource-Based, but Special)

KMS key policies are the **one resource-based policy type that is checked by default even for the key's own account** — this is a deliberate KMS design choice, unlike most other resource-based policies.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "EnableRootAccountFullAccess",
      "Effect": "Allow",
      "Principal": { "AWS": "arn:aws:iam::123456789012:root" },
      "Action": "kms:*",
      "Resource": "*"
    },
    {
      "Sid": "AllowUseOfKeyForEncryptDecrypt",
      "Effect": "Allow",
      "Principal": { "AWS": "arn:aws:iam::123456789012:role/AppRole" },
      "Action": [
        "kms:Encrypt",
        "kms:Decrypt",
        "kms:GenerateDataKey"
      ],
      "Resource": "*"
    }
  ]
}
```

**Why the first statement (root access) matters**: unlike most resource policies, a KMS key policy that doesn't grant the account root at least some access can lock the key management out of IAM entirely — the account root statement is what allows the key's permissions to *also* be managed via IAM identity-based policies layered on top. Without it, only whatever's explicitly in the key policy applies.

**`Resource: "*"` in a KMS key policy is normal and expected** — unlike almost every other policy type, `*` here means "this key" (the policy is already scoped to the key it's attached to), not "every resource in the account." Don't flag this as a least-privilege violation on the exam the way you would for an IAM policy.

**Exam-relevant KMS distinction**: `kms:Encrypt`/`kms:Decrypt` operate on data directly (limited to 4KB), while `kms:GenerateDataKey` is the operation behind envelope encryption — it returns a data key used to encrypt your actual (larger) payload, with the data key itself encrypted by the CMK. Questions about "how does S3 SSE-KMS handle objects larger than 4KB" are testing whether you know this GenerateDataKey mechanism exists.

---

## 7. IAM Trust Policies (a special resource-based policy attached to Roles)

A trust policy is technically the "resource-based policy" attached to an IAM **role** — it defines *who is allowed to assume the role*, separate from the role's *permission* policy (what the role can do once assumed).

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": { "Service": "lambda.amazonaws.com" },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

or for cross-account:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": { "AWS": "arn:aws:iam::999999999999:root" },
      "Action": "sts:AssumeRole",
      "Condition": {
        "StringEquals": { "sts:ExternalId": "unique-shared-secret-123" }
      }
    }
  ]
}
```

**Every IAM role has exactly two policies attached to it**, and mixing them up is a very common exam trap:
1. **Trust policy** — WHO can assume this role (`sts:AssumeRole` as the Action, a `Principal` — service or account — as the who)
2. **Permission policy** (one or more) — WHAT the role can do once assumed (looks like a normal identity-based policy)

**`ExternalId` condition**: used specifically for third-party cross-account access (e.g., a SaaS vendor assuming a role in your account) to prevent the "confused deputy" problem, where a third party could be tricked into acting on behalf of an account it shouldn't. If a scenario mentions a third-party vendor needing role access to your account, `ExternalId` is very likely the expected answer element.

---

## 8. Service Control Policies (SCPs) — Organization-Level Ceiling

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "ec2:*",
      "Resource": "*",
      "Condition": {
        "StringNotEquals": { "aws:RequestedRegion": ["us-east-1", "ap-south-1"] }
      }
    }
  ]
}
```

**SCPs almost always appear as `Deny` statements in real usage**, even though `Allow` is syntactically valid. Why: SCPs set the **maximum available permissions** for accounts/OUs in an Organization — they never grant anything by themselves. An identity-based policy inside the account still has to separately grant the actual permission; the SCP just caps what's possible. This mirrors the Permission Boundary logic in section 4, just at the organization level instead of the account level.

**SCPs do not apply to the organization's management (payer) account** — a frequently tested gotcha.

---

## 9. Syntax & Structural Traps — Quick Checklist

Run through this whenever the exam shows you raw policy JSON:

- [ ] Is `Principal` present when it should be (resource-based/trust policy) or absent when it should be (identity-based policy)?
- [ ] Does the `Resource` ARN match the action's actual target level — bucket-level ARN for bucket actions, `/*` object-level ARN for object actions?
- [ ] Are there duplicate `Sid` values in the same policy document?
- [ ] Is `Action` using valid `service:ActionName` syntax — no stray extra colons, no typos in the service prefix?
- [ ] Is a `Deny` statement scoped precisely, or does it accidentally block more than intended?
- [ ] Does a `Condition` block use the right operator (`StringEquals` vs `StringNotEquals`, `IpAddress` vs `NotIpAddress`) for the intent described?
- [ ] For cross-account scenarios: does *both* sides' policy allow it, or does the design rely on a resource policy/role that only needs one side?

---

## 10. Practice Questions

**Q1.** A company's S3 bucket policy grants `s3:GetObject` to a specific external AWS account, but users in that account still cannot download objects even though their own IAM policies allow `s3:GetObject` on that bucket. What is the MOST likely cause?

A. The bucket policy is missing a `Principal` element
B. The external account's IAM policy is missing a `Resource` element
C. The bucket owner's account has not enabled cross-account access at the account level
D. The object ACLs still list the bucket owner as the sole owner, blocking access regardless of policy

<details><summary>Answer & Explanation</summary>

**D.** When objects are uploaded by the bucket owner but the *object* ACL still restricts ownership/access exclusively to the uploading account, a bucket policy alone can be insufficient in ACL-enabled buckets — this is the classic "bucket policy says yes, object ACL says no" conflict. (Modern best practice: enable S3 Object Ownership "Bucket owner enforced" to disable ACLs entirely and rely purely on policies — but the exam still tests recognizing this failure mode.)
- A is wrong because if `Principal` were missing, the bucket policy itself would fail to apply/save (as you saw in your practice test), not silently allow-but-fail at download time.
- B is a red herring — IAM policies commonly use `Resource: "*"` or the correct ARN; a missing Resource would cause a validation error, not a silent runtime failure.
- C describes something that isn't a real, distinct AWS setting — there's no separate account-level cross-account toggle beyond the policies themselves.
</details>

**Q2.** A KMS key policy contains only one statement granting a specific application role `kms:Encrypt` and `kms:Decrypt`, with no statement referencing the account root. An administrator with full `AdministratorAccess` IAM policy attached is unable to modify the key's policy. Why?

A. KMS key policies always ignore IAM administrator policies
B. Without a statement granting the account root access, the key policy is the only source of permissions for that key, and IAM policies cannot layer on top
C. The administrator needs `kms:PutKeyPolicy` explicitly listed in the key policy itself, regardless of root access
D. KMS keys can only be modified via the AWS root user, never IAM

<details><summary>Answer & Explanation</summary>

**B.** This is the core exam-relevant KMS behavior: unlike most resource-based policies, a KMS key policy is authoritative by default. The account root grant is what "opens the door" for IAM identity-based policies elsewhere in the account (like the administrator's `AdministratorAccess` policy) to also apply to the key. Without it, only the exact statements in the key policy govern access — full stop.
- A is too absolute — IAM policies *can* apply to KMS keys, just only when the key policy grants root the ability to delegate that way.
- C is a plausible-sounding trap, but it's the root-account delegation that's structurally required, not a specific action name.
- D is factually wrong — IAM users/roles routinely manage KMS keys once the delegation via root is in place.
</details>

**Q3.** A company wants a third-party SaaS vendor to assume a role in its AWS account to pull billing data, without risking the vendor's role credentials being reused by an unrelated party who somehow learns the role ARN. Which trust policy element should be used?

A. A `Condition` requiring `aws:MultiFactorAuthPresent`
B. A `Condition` using `sts:ExternalId` with a unique, pre-shared value
C. A `Principal` restricted to a specific IP range
D. A permission boundary attached to the vendor's IAM role in their own account

<details><summary>Answer & Explanation</summary>

**B.** This is exactly the "confused deputy" problem `ExternalId` was designed for — a shared secret embedded in the trust policy's condition, known only to the account owner and the specific vendor, ensures that even if a third, unrelated party discovers the role ARN, they can't successfully assume it without also knowing the ExternalId.
- A is a real security control but solves a different problem (proving human presence via MFA), not third-party identity confusion.
- C doesn't make sense for a SaaS vendor calling from their own infrastructure with unpredictable source IPs.
- D operates entirely in the vendor's own account and has no bearing on who can assume a role in *your* account.
</details>

**Q4.** An SCP attached to an Organizational Unit denies `s3:DeleteBucket` for all accounts in that OU. An account within the OU has an IAM policy explicitly allowing `s3:DeleteBucket` for a specific administrator role. Can that administrator delete buckets in that account?

A. Yes, because explicit IAM Allow always overrides SCP Deny
B. No, because SCPs set the maximum permissions ceiling — an explicit Deny at the SCP level cannot be overridden by any identity-based policy inside the account
C. Yes, but only if the administrator also has a permission boundary explicitly allowing it
D. It depends on whether the SCP was applied before or after the IAM policy was created

<details><summary>Answer & Explanation</summary>

**B.** SCPs are a hard ceiling evaluated independently of anything inside the account. Per the evaluation logic in section 3, an explicit Deny anywhere in the applicable policy set (which includes SCPs) always wins, with zero exceptions. No IAM policy inside the account, however permissive, can override an SCP-level Deny.
- A directly contradicts the "explicit Deny always wins" rule.
- C is a distractor mixing up permission boundaries (account-level ceiling) with SCPs (org-level ceiling) — a boundary can't override an SCP either.
- D is a trap — evaluation order at request time doesn't depend on creation timestamps; all applicable policies are evaluated together for each request.
</details>

**Q5.** A bucket policy statement uses `"Resource": "arn:aws:s3:::reports-bucket"` (no trailing `/*`) with `"Action": "s3:GetObject"`. Users report `AccessDenied` errors when trying to download files, even though the policy appears to grant read access. What's wrong?

A. `s3:GetObject` requires `Principal` to be a wildcard `*`
B. The `Resource` ARN targets the bucket itself, but `s3:GetObject` is an object-level action and needs the ARN to end in `/*`
C. The `Version` field is outdated and should be `2008-10-17`
D. `s3:GetObject` cannot be granted via bucket policy, only via IAM policy

<details><summary>Answer & Explanation</summary>

**B.** This is the single most common real-world (and exam) S3 policy mistake: bucket-level actions (`s3:ListBucket`, `s3:GetBucketLocation`) target the bucket ARN itself; object-level actions (`s3:GetObject`, `s3:PutObject`, `s3:DeleteObject`) need the ARN extended with `/*` to cover the objects inside the bucket. Without it, the statement is syntactically valid but never actually matches any object, resulting in access denied.
- A is fabricated — Principal scope and Action requirements are unrelated.
- C is backwards — `2012-10-17` is the current version; `2008-10-17` is the legacy one.
- D is false — bucket policies routinely grant object-level actions; that's one of their primary uses.
</details>

---

*Cross-reference: when you get a policy question wrong in future mocks, check it against the section 9 checklist first — most policy-syntax misses trace back to one of those seven checks specifically.*
