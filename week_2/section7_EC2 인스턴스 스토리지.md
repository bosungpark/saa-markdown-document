EBS 개요
-
- An EBS(Elastic Block Store) volume is a network drive you can attach to your instance while they are running.
- It allow your instanse to persist data even after their termination.
- They only can mounted to one instance at a time
- They are bound to a specific Availablity Zone.


- EBS Volume
  - It is a Network Drive not Physical


EBS Snapshots
-
- Make a backup of your EBS volume at a point of time
- Not necessary to detach volume to do snapshot but recommended
- Can copy snapshot across Region or AZ

AMI
-
- AMI(Amazon Machine Image)
- AMI are a customization of an EC@ instance
  - You add your own software, configuration, os, monitoering...
  - Faster boot/ configuration time because all your software is pre-packaged
- AMI are built for a specific region (and can be copied across regions)


1. Start an EC2 instance and customize it
2. Stop the instance (for data integrity)
3. Build an AMI - this will also create EBS snapshot
4. Launch instances from other AMIs

EC2 Instance Store
-
- EBS volumes are network drive with good but "limited" performance
- If you need a high-performance hardware disk, use EC2 Instance Store
  - Better I/O performance
  - EC2 Instance Store lose storage if they are stopped
  - Good for buffer / cache / scratch data / temporary content
  - Risk of data loss if hardware fails
  - Backups and Replication are your Responsibility

EBS Volumes
-
- see video

EBS Multi Attach
-
- Attach the same EBS volume to multiple EC2 instances in the same AZ
- Each instance has full read and write permissions to high-performace volume
- Up to **16** EC2 Instances at a time
- Must use a file system that's cluster-aware

EBS Encryption
-
- When you create an encrypted EBS volume, you get following:
  - Data at rest is encrypted inside the volume
  - All the data in flight moving between the instance and the volume is encrypted
  - All snapshots are encrypted
  - All volumes created from snapshot
- Encryption and decryption are handled transparently
- Encryption has a minimal impact on latency
- EBS Encryption leverages keys from KMS(AES-256)
- Copying an unencrypted snapahot allows encryption
- Snapshots of encrypted volumes are encrypted


1. Create an EBS snapshot of volume
2. Encrypt the EBS snapshot (using copy)
3. Create new ebs volume from the snapshot (the volume will also be encrypted)
4. Now you can attach the encrypted volume to the original instance

Amazon EFS - Elastic File System
-
- Manage NFS(Network file system) that can be mounted on many EC2
- EFS works with EC2 instances in multi-AZ
- Highly available, scalable, expensive, pay per use
- Compatible with Linux based AMI
- Uses NFSv4.1, security group, encryption at rest using KMS

EBS, EFS
-
- EBS
  - can be attached to only one instance at a time
  - are locked at AZ level
  - I/O increases if the disk size increases
  - can increase I/O independently
- EFS
  - Mounting 100s of instances across AZ
  - EFS share websit files
  - Only for Linux Instances
  - EFS has a higher price point than EBS
  - Can leverage EFS-IA for cost saving