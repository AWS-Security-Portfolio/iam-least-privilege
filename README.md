## AWS IAM & Least Privilege Lab

Designed granular IAM policies and role-based access for secure AWS resource isolation.

---

## Table of Contents

- [Overview]
- [Objectives]
- [Steps Performed]
  - [1. Root Account and Admin Setup]
  - [2. IAM Users, Groups, and Roles]
  - [3. Policy Authoring and Attachment]
  - [4. Security Group and Key Pair Creation]
  - [5. EC2 Launch and Role Attachment]
  - [6. Access Verification and Testing]
- [Screenshots]
- [Lessons Learned]
- [References]

---

## Overview

This project demonstrates the design and enforcement of AWS Identity and Access Management (IAM) using the principle of least privilege. The lab covers the creation of IAM users, groups, roles, and custom JSON policies, as well as configuring EC2 instance roles and SSH/network access controls. The outcome is a securely segmented AWS environment, with documented evidence for each step.

![Lab Diagram](.diagram.png)

---

## Objectives

- Secure the AWS root account with MFA.
- Create a dedicated admin IAM user.
- Set up IAM users (`S3User`, `EC2User`, `DenyUser`) for resource isolation.
- Create groups and roles as appropriate for permissions management.
- Author and attach least privilege JSON policies.
- Launch an EC2 instance with a restrictive security group and an IAM role for S3.
- Demonstrate permission enforcement through testing and screenshots.

---

## Steps Performed

1. Root Account and Admin Setup  
   - Enabled MFA on the AWS root account.  
   - Created a new admin IAM user with AdministratorAccess policy.

2. IAM Users, Groups, and Roles.  
   - Created 'S3User', 'EC2User' and 'DenyUser'.  
   - Created IAM groups for S3 and EC2 access (Optional) 
   - Created an IAM role for EC2 (with S3 permissions)

3. Policy Authoring and Attachment  
   - Authored custom JSON policies for S3, EC2, and deny access.  
   - Attached policies to the appropriate users, groups, and role.

4. Security Group and Key Pair Creation  
   - Created a security group allowing SSH from a specific IP.  
   - Generated an EC2 key pair for secure SSH access.

5. EC2 Launch and Role Attachment  
   - Launched a new EC2 instance using Amazon Linux.  
   - Attached the IAM role and security group to the instance.

6. Access Verification and Testing  
   - Verified IAM user permissions via the AWS Console.  
   - Connected to the EC2 instance via SSH.  
   - Tested S3 access from the instance to confirm least privilege.  
   - Collected screenshots as evidence for each stage.

---

## Screenshots

*All relevant screenshots demonstrating each step are included in the screenshots/ folder of this repository.

| #  | File Name                          | What it Shows                                       |
|----|------------------------------------|-----------------------------------------------------|
| 1  | s3user-s3-allowed.png              | S3User successfully accessing S3 (allowed action)   |
| 2  | s3user-ec2-denied.png              | S3User denied when trying to access EC2             |
| 3  | ec2user-ec2-limited-success.png    | EC2User accessing EC2 with limited permissions      |
| 4  | ec2user-s3-denied.png              | EC2User denied when trying to access S3             |
| 5  | ec2-instance-details.png           | EC2 instance details (shows IAM role, security group)|
| 6  | ec2-s3-access-denied.png           | EC2 (with role) denied when attempting S3 action    |
| 7  | ec2-security-group-mypionly.png    | Security group allowing SSH only from my IP         |
| 8  | ec2-security-group-rules.png       | Security group inbound rule details                 |
| 9  | ec2-security-group-settings.png    | General security group configuration                |
| 10 | denyuser-ec2-denied.png            | DenyUser denied when trying to access EC2           |
| 11 | denyuser-s3-denied.png             | DenyUser denied when trying to access S3            |

### Screenshot Explanations

1. s3user-s3-allowed.png  
   Proof that S3User can access S3 as permitted by the least-privilege policy.

2. s3user-ec2-denied.png
   Shows S3User is denied access to EC2 resources, as intended.

3. ec2user-ec2-limited-success.png  
   Demonstrates EC2User can access EC2 dashboard and perform limited actions.

4. ec2user-s3-denied.png 
   Shows EC2User is denied access to S3, enforcing separation of duties.

5. ec2-instance-details.png  
   Displays EC2 instance with attached IAM role and associated security group.

6. ec2-s3-access-denied.png 
   Terminal output: EC2 instance (with role) is denied S3 access, validating least privilege.

7. ec2-security-group-mypionly.png  
   Screenshot showing security group configured to allow SSH only from my IP address.

8. ec2-security-group-rules.png
   Details of the inbound rules for the EC2 security group.

9. ec2-security-group-settings.png  
   General configuration for the security group used in the lab.

10. denyuser-ec2-denied.png  
    DenyUser receives “Access Denied” when attempting to access EC2 resources.

11. denyuser-s3-denied.png 
    DenyUser receives “Access Denied” when attempting to access S3 resources.

---

## Lessons Learned

- Planning and enforcing least privilege is critical for AWS security.
- MFA and separation of duties reduce risks on critical accounts.
- Using roles for EC2 access is more secure than access keys.
- Testing each user and role from the console and CLI is essential.
- Documenting every stage (including failures/access denied) proves security posture and provides clarity for auditors or recruiters.

---

## References

- AWS IAM Documentation  
  https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html

- AWS EC2 Documentation  
  https://docs.aws.amazon.com/ec2/

- AWS Security Best Practices  
  https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-standards-fsbp.html

---

Sebastian Silva C. – July, 2025 – Berlin, Germany.
