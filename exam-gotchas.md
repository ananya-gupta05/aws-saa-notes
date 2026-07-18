# Exam Gotchas & Random Discoveries

Running log of specific things I stumble on during practice tests — the kind of detail that's easy to miss but shows up as a trick question.

## Macie doesn't scan RDS — use Glue DataBrew instead
- **Macie** only scans data in **S3** for PII/sensitive data detection — it does NOT work directly on RDS
- If you need PII detection on data sitting in **RDS**, the answer is **AWS Glue DataBrew** — it has built-in PII statistics/detection transforms you can run on RDS-sourced data
- Exam trap: if a question mentions PII detection + RDS in the same breath, Macie is the wrong-sounding-right answer — DataBrew is correct

## VPC Peering vs VPC Sharing
- **VPC Peering**: connects two *separate* VPCs (same or different accounts) so resources can talk to each other privately. Each VPC keeps its own subnets, route tables, resources — peering just links them at the network level. No transitive peering (if A↔B and B↔C, A cannot reach C automatically).
- **VPC Sharing** (via AWS Resource Access Manager): a *single* VPC's subnets are shared across multiple AWS accounts within an Organization. Participant accounts can launch resources directly into the shared subnets — it's one VPC being used by many accounts, not two VPCs being linked.
- Exam trap: peering = two VPCs staying separate but connected. Sharing = one VPC, multiple accounts using its subnets directly.

## EKS Managed Node Groups for containerized workloads
- **EKS Managed Node Groups** = AWS handles provisioning, patching, and lifecycle of the EC2 worker nodes for your EKS cluster — you don't manually manage the underlying instances
- Good "fully managed" answer whenever a question wants containerized workloads on Kubernetes without the ops overhead of self-managed nodes
- Compare against:
  - **Self-managed nodes** — you provision/patch the EC2 instances yourself, more control but more overhead
  - **Fargate for EKS** — no nodes at all, fully serverless, AWS manages everything including the underlying compute (goes a step further than managed node groups)
- Exam trap: if the question emphasizes "least operational overhead" + Kubernetes/containers, Fargate is usually more correct than Managed Node Groups. Managed Node Groups is the answer when you still need some control (e.g., custom AMIs, GPU instances) but don't want to handle patching/scaling yourself.

## WAF for DDoS mitigation — Layer 7 only
- **AWS WAF** can help mitigate DDoS attacks, but only at **Layer 7** (application layer) — e.g. HTTP floods, malicious request patterns, rate-based rules blocking abusive IPs
- WAF does NOT protect against **Layer 3/4** (network/transport layer) attacks like SYN floods or UDP reflection attacks
- For Layer 3/4 protection, that's **AWS Shield** (Standard is automatic/free for all customers; Advanced adds more protection + 24/7 DDoS response team + cost protection)
- Exam trap: if the question is about a volumetric/network-layer DDoS attack, WAF alone is NOT the right answer — you need Shield (often paired with WAF for full-stack protection, since they commonly work together: Shield for L3/L4, WAF for L7)
