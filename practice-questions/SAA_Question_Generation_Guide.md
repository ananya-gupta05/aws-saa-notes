# SAA-C03 Practice Question Generator — Instructions for AI

Use this document as a system prompt / instruction set for any AI you want to generate AWS SAA-C03-style practice questions. It's built from analyzing the structure of an official-style 65-question practice set against the real AWS exam guide (v1.1) — not by copying any specific question, but by extracting the *pattern* that makes these questions hard in the right way.

---

## 1. Domain Distribution (must be respected across any batch of questions)

When generating a batch of N questions, distribute them as:
- **Domain 1 — Design Secure Architectures: 30%** (secure access/IAM, secure workloads/network controls, data security controls)
- **Domain 2 — Design Resilient Architectures: 26%** (scalable/loosely-coupled design, high availability/fault tolerance, DR strategies)
- **Domain 3 — Design High-Performing Architectures: 24%** (storage performance, compute performance/elasticity, database performance, networking performance)
- **Domain 4 — Design Cost-Optimized Architectures: 20%** (cost-effective storage, compute, database, network solutions)

For a 65-question set: roughly 19-20 / 17 / 15-16 / 13 questions respectively.

## 2. Question Anatomy (every question should follow this shape)

1. **Scenario paragraph** — 2-4 sentences establishing a company/application context. Include at least one specific, concrete number (traffic rate, data size, time window, RPO/RTO, cost figure, item size) that is *load-bearing* — i.e., the correct answer changes depending on that number, it's not just flavor text.
2. **Constraint sentence(s)** — one or two sentences stating the actual requirement(s): security posture, availability target, performance target, or cost ceiling. This is the real question; the scenario paragraph is context for evaluating it.
3. **The question itself, ending in a superlative or qualifier**: "MOST secure," "MOST cost-effective," "LEAST operational overhead," "with the HIGHEST throughput," "FASTEST," "with minimal disruption," "without downtime." Never end on a bare "what should be done" without a qualifier — the qualifier is what makes multiple technically-valid answers resolvable to one correct answer.
4. **Four answer options** (or five with "Select TWO" — see section 4), each a *complete solution*, not a single service name in isolation. Good options describe a mechanism ("Create X, configure Y to do Z"), not just "Use CloudFront."

## 3. Distractor Design Patterns (use 2-3 of these per question, mixed)

**A. Technically functional but violates a stated constraint.**
The distractor solves the general problem but ignores one specific word in the constraint sentence — usually the superlative or a secondary requirement mentioned once, early, and never repeated. Example pattern: scenario demands "least operational overhead," distractor proposes a self-managed EC2/cron solution that works but requires ongoing patching/scaling management.

**B. Right service family, wrong applicability.**
Propose a control or feature that doesn't actually apply to the resource type in question — e.g., a network-layer construct (Security Group/NACL) applied to a resource that isn't deployed inside a VPC context, or a resource-level policy pattern applied where only an identity-level one works. Tests whether the test-taker knows *where* a mechanism operates, not just that it exists.

**C. Cross-service API/feature name swap.**
Take a real, specific AWS API operation or named feature and pair it with the *wrong* AWS service in the option text (a feature that belongs to Service X attached to Service Y in the distractor). This tests precise service boundaries, not just general awareness. Only usable where the AI generating the question is confident of the real API names — do not invent fictional API names.

**D. Solves a different (adjacent) problem than the one asked.**
E.g., a distractor addressing durability when the question asks about availability; addressing encryption-in-transit when the question asks about encryption-at-rest; addressing RPO when the question specifies RTO. These pairs are easy to confuse and make excellent distractors precisely because both concepts are "correct sounding."

**E. Requires downtime/disruption when the constraint says there must be none.**
Common in database/storage questions: a distractor that requires deleting and recreating a resource, or a cutover with a service interruption, when the scenario specifies "without downtime" or "with minimal disruption to running applications."

**F. Uses deprecated or superseded terminology/approach.**
E.g., an older mechanism that AWS has functionally replaced with a better one (the older one may still technically work, but a newer purpose-built feature is the better/expected answer). Good for the "know the current best practice" test AWS favors.

**G. Overly broad or overly narrow security scoping.**
Options using `0.0.0.0/0` where a scoped source is needed, or a security control applied to too broad or too narrow a boundary (VPC-wide vs instance-level vs subnet-level) relative to what the scenario specifies.

**H. Numeric/threshold math traps.**
For cost or performance questions, embed numbers that require actual computation to resolve — e.g., "if this change causes runtime to drop below X seconds" paired with a cost-per-GB-second model, where the test-taker must verify whether the tradeoff is actually net-positive, not just directionally plausible.

## 4. "Select TWO" / "Select THREE" Questions

- Never construct these as "two clearly correct, two clearly wrong." Structure as: **one obviously wrong** (wrong service category entirely), **one that addresses a different problem** than the one stated, and **two-to-three genuinely plausible options** where only the required number are fully correct — the difference usually hinging on one of the distractor patterns above (commonly pattern D or E).
- Both correct answers, together, should form a *coherent combined solution* — not two independent unrelated fixes.

## 5. Numeric/Limit Emphasis (do this deliberately — it's a defining feature of this exam)

Bake in real, correct AWS service limits and defaults as load-bearing plot points, not decoration:
- Data/request volumes near a real throughput or throttling limit (RCU/WCU, API Gateway throttle defaults, SQS message size)
- Time windows tied to real feature behavior (S3 Glacier retrieval tiers, RDS backup retention defaults, DynamoDB PITR window)
- Explicit RPO/RTO numbers that map onto a specific DR strategy (Backup & Restore / Pilot Light / Warm Standby / Multi-Site Active-Active) — force the reader to infer the strategy from the numbers rather than naming it directly
- Cost or size figures that only make sense with one storage class, instance purchasing option, or capacity mode

**Do not invent limits.** If generating with an AI, instruct it to only use real, verifiable AWS service limits and defaults — a wrong invented limit undermines the whole question's validity. Where unsure, it should default to a scenario that doesn't hinge on a specific number rather than fabricate one.

## 6. Style & Language Conventions

- Use real, exact AWS service and feature names (not colloquial names) — e.g., "Amazon Elastic Container Service (Amazon ECS)" on first mention, "ECS" after.
- Prefer scenarios framed around a named company/team/application rather than abstract "you need to..." phrasing.
- Vary the superlative used across a batch — don't let every question in a set end on "MOST cost-effective."
- Occasionally include a short IAM policy JSON snippet or CLI-style resource identifier as part of the scenario or an answer option, with a subtle, realistic syntax or semantic error (missing `Principal`, wrong `Resource` ARN pattern, duplicate `Sid`, incorrect `Effect`) for policy-literacy testing — sparingly, 1 in every 15-20 questions.
- Each of the four domains should have its own flavor of "correct answer profile": Domain 1 answers tend to converge on IAM roles over long-lived credentials, resource policies for cross-account, and VPC endpoints over internet routes. Domain 2 answers converge on decoupling (SQS/SNS/EventBridge), multi-AZ design, and matching DR strategy to RTO/RPO. Domain 3 answers converge on the right storage/database primitive for the access pattern and the right caching layer. Domain 4 answers converge on right-sizing, the correct purchasing option, and serverless/pay-per-use for spiky/intermittent workloads.

## 7. Prompt Template to Hand to an AI Question Generator

```
Generate [N] AWS SAA-C03-style multiple-choice practice questions.

Distribute across domains: 30% Domain 1 (Secure Architectures), 26% Domain 2
(Resilient Architectures), 24% Domain 3 (High-Performing Architectures),
20% Domain 4 (Cost-Optimized Architectures), per the official SAA-C03 exam
guide v1.1 task statements.

For each question:
- Write a 2-4 sentence scenario with at least one load-bearing concrete number
  (traffic rate, data size, time window, RPO/RTO, or cost figure) that changes
  which answer is correct.
- State the constraint/requirement explicitly in 1-2 sentences.
- End the question on a superlative: MOST secure / MOST cost-effective /
  LEAST operational overhead / HIGHEST throughput / FASTEST / with minimal
  disruption / without downtime — vary this across the set.
- Provide 4 complete-solution answer options (each describing a mechanism,
  not just naming a service). Use exactly ONE correct answer per question,
  except for a mix of "Select TWO" questions structured as: 5 options, one
  clearly wrong, one solving a different but adjacent problem, and two-to-
  three plausible options where only two are fully correct together.
- Use ONLY real, verifiable AWS service names, API operation names, and
  service limits/defaults. Do not invent limits, API names, or features.
- Build distractors using these patterns (mix 2-3 per question):
  (a) technically functional but violates the stated superlative/constraint
  (b) right service family, wrong applicability/boundary
  (c) real API/feature name attached to the wrong AWS service
  (d) solves an adjacent but different problem (durability vs availability,
      encryption in-transit vs at-rest, RPO vs RTO)
  (e) requires downtime when the scenario specifies none
  (f) uses a deprecated/superseded approach instead of the current
      best-practice service/feature
  (g) overly broad or narrow security scoping
  (h) a numeric/cost tradeoff that requires actual computation to resolve

After each question, provide: the correct answer, a 2-3 sentence explanation
of why it's correct, and a one-line explanation for why EACH distractor is
wrong (tie each to one of the patterns above).
```

## 8. Self-Check Before Using Generated Questions

- Does the scenario contain a number that actually matters, or is it decorative?
- Does the question end on a superlative that's checkable against every option?
- Are all four options *solutions*, not bare service names?
- Do the distractors fail for a *specific, statable reason* tied to one pattern above — not just "because it's wrong"?
- Are all service names, API names, and limits real and correct? (If generating with an AI, spot-check a few against current AWS documentation before trusting a batch — models can still invent plausible-sounding but wrong limits.)
- Does the batch's domain distribution roughly match 30/26/24/20?
