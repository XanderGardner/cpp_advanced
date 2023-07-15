# AWS
- [Back to Main](README.md)

- [the cloud](#the-cloud)

---

# the cloud

hypervisor: program used to manage one or more VMs on a computer
cloud hypervisor: used to manage many VMs using the cloud providor's resources

Cloud computing models:
- IaaS: Infastructure as a service, where users have the most control over resources, such as AWS.
- PaaS: Platform as a service, where users can host applications, such as Heroku
- SaaS: Software as a service, where users can simply create an account to use the service, such as Microsoft Office

Cloud computing deployments:
- Cloud deployment: all IT infastructure lives on the cloud
- On-premises deployment: IT infastructure, such as servers, is owned by the organization and virtualized (private cloud)
- Hybrid deployment: some cloud and some owned infastructure

Services:
- Computing
  - virtual server hosting, container management, serverless computing
  - lambda: run code on triggers
  - EC2: Elastic Compute Cloud used to run virtual machines
  - LightSail: setup small websites
  - ECS: Elastic Container Service used to ship software to users
- Storage:
  - storage for in-use and archival files
  - EFS: Elastic File System used to create shared folders
  - S3: Simple Storage Service used to link files to website
  - Glacier: storage large amounts of data for cheap
  - Storage Gateway: safekeeping on-premise data
- Database:
  - RDS: relational database service
  - DynamoDB: noSQL database
  - RedShift: petabyte scale database service
  - ElastiCache: scalable caching service for expensive computations

# IAM
- security service: "identity and access management"
- each user has an associated policies, which are defined permissions
- policy: defined list of permissions
- group: defined list of users that have set policies
- roles: defined set of policies that service can have when running
