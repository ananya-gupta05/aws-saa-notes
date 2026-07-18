# Amazon FSx & AWS Snowball

## Amazon FSx
- Managed file storage service, gives you native file systems instead of object storage like S3
- Two main flavors:
  - **FSx for Windows File Server** — SMB protocol, integrates with Active Directory, good for Windows-based workloads
  - **FSx for Lustre** — high-performance file system for compute-intensive workloads (ML, HPC, big data)
- Exam trap: don't confuse with EFS — EFS is Linux/NFS-based, FSx for Windows is SMB-based

## AWS Snowball
- Physical device used to migrate large amounts of data (terabytes to petabytes) into/out of AWS
- Used when transferring over the network would take too long or be too costly
- Variants:
  - **Snowball Edge (Storage Optimized)** — bulk data transfer + local storage
  - **Snowball Edge (Compute Optimized)** — data transfer + edge compute/ML inference
  - **Snowcone** — smaller, portable version for lighter workloads
  - **Snowmobile** — truck-sized, for exabyte-scale migrations
- Exam trap: rule of thumb — if it would take more than ~1 week to transfer over your network connection, Snowball is usually the better choice over Direct Connect/internet transfer
