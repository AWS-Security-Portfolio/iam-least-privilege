# AWS IAM & Least Privilege Lab

## Overview

This project demonstrates the design and implementation of AWS Identity and Access Management (IAM) following the principle of least privilege. The goal was to create multiple users and roles with granular permissions, set up EC2 instance access with appropriate IAM roles, and document evidence of correct access controls. See the diagram below for a high-level view of the users, roles, and resources involved in this lab.

---

## Architecture Diagram

The diagram below illustrates the main components and relationships in this IAM & Least Privilege lab.

![aws-iamlab-sebastiansilva](diagram.png)


## Objectives

- Understand and apply AWS IAM concepts: users, groups, roles, policies
- Enforce least privilege on users and roles
- Enable secure access to EC2 and S3 resources
- Demonstrate restricted access using security groups and IAM policies
- Document and verify access results

---

## Users, Roles, and Policies

- **Users:**  
  - `S3User`: Intended to access S3 only
  - `EC2User`: Intended to access EC2 only
  - `DenyUser`: Should not have access to EC2 or S3


| User      |S3 Access|EC2 Access | Expected Result    |
|-----------|---------|-----------|--------------------|
| S3User    | Granted |  Denied   | Can access S3 only |
| EC2User   | Denied  | Granted   | Can access EC2 only|
| DenyUser  | Denied  |  Denied   | No access granted  |


- **Groups:**  
  - `S3Team` (optional): S3 access policy.
  - `EC2Team` (optional): EC2 access policy.

- **Roles:**  
  - `EC2S3AccessRole`: Attached to EC2 instance, controls S3 access from EC2.

- **Policies:**  
  - Custom JSON policies attached to each user, group, or role.




---

## Lab Steps

1. **Root Account Hardening:**  
   - Set up MFA on root account  
   - Created individual admin IAM user with full permissions

2. **User, Group, and Role Creation:**  
   - Created S3User, EC2User, DenyUser  
   - (Optional) Created groups for S3 and EC2 access  
   - Attached custom policies enforcing least privilege

3. **Policy Attachment:**  
   - Uploaded policies to AWS IAM and attached as required  
   - Verified policy effect by logging in as each user

4. **Security Group Setup:**  
   - Created a security group allowing SSH only from any IP address

5. **EC2 Launch and IAM Role:**  
   - Created key pair for SSH  
   - Launched EC2 instance with correct IAM role attached  
   - Attached the security group

6. **Access Verification & Testing:**  
   - SSH’ed into EC2  
   - Ran AWS CLI commands to test access  
   - Verified correct access denied where appropriate

7. **Documentation:**  
   - Took screenshots at each step as evidence (see `/screenshots/` folder)  
   - Saved IAM policy JSON files (see `/policies/` folder)

---

## Results

- **Least privilege enforced**:  
  - Users only have access to their assigned services (or none, in the case of DenyUser)
  - EC2 instance access is restricted via security group and IAM role
  - S3 access denied as expected from EC2 instance (see screenshot)
- **Root account is secured with MFA and not used for daily tasks**
- All steps are documented with clear screenshots

---

## Screenshots

Screenshots of all key steps are available in the `/screenshots` folder, including:
- User, group, role, and policy creation
- Security group configuration
- EC2 instance details
- Successful and denied access attempts

---

## Policies

All JSON IAM policies are provided in the `/policies` folder.  
Refer to these if you want to reuse or inspect the policy definitions.

---

## Takeaways

- Following least privilege in AWS is straightforward but requires careful planning of policies
- Attaching IAM roles to EC2 is critical for secure automation
- Always verify your permissions by testing with AWS CLI or Console access
- Security groups are your first line of network defense in AWS

---

## Tagline

> Designed granular IAM policies and role-based access for secure AWS resource isolation.



