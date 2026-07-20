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

## DAX vs ElastiCache for DynamoDB caching
- **DAX (DynamoDB Accelerator)**: purpose-built caching layer specifically for DynamoDB. Sits in front of DynamoDB, microsecond latency, and is **API-compatible** with DynamoDB — meaning little to no code changes needed to adopt it
- **ElastiCache** (Redis/Memcached): general-purpose caching, works with any database/data source — but using it in front of DynamoDB requires you to **manually write caching logic** in your application code (check cache → miss → query DynamoDB → write to cache)
- Exam trap: if the question is specifically about caching for DynamoDB with minimal code change / minimal operational overhead, DAX is the correct answer over ElastiCache. ElastiCache is the better answer when caching needs to sit in front of multiple/non-DynamoDB data sources, or when more caching control/flexibility is needed.

## Transit Gateway vs VPC Peering for many-to-many VPC connectivity
- **VPC Peering** doesn't scale well for many VPCs needing to talk to each other — no transitive routing, so you'd need a separate peering connection between every single pair (mesh). E.g. 10 VPCs all talking to each other = 45 peering connections. Becomes unmanageable fast.
- **Transit Gateway** solves this: acts as a central hub, each VPC attaches to it once, and it handles routing between all attached VPCs — no full mesh needed
- Use **route tables on the Transit Gateway** to control which VPCs can reach which — e.g. if only 5 of 10 VPCs should see all others, and the remaining 5 should only reach a subset, you create separate TGW route tables and associate/propagate routes selectively per attachment, instead of physically blocking with dozens of peering connections
- Exam trap: whenever the question describes multiple VPCs (roughly 4-5+) needing selective or full interconnectivity, Transit Gateway is almost always the better/correct answer over a peering mesh — peering is fine for just 2, maybe 3 VPCs, but doesn't scale









