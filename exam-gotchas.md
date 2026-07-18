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
