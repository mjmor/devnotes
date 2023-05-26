---
layout: default
title: AWS
nav_order: 1
permalink: /dev-ops/aws
parent: DevOps
has_children: true
---

# Amazon Web Services (AWS)

Command environment configurations and build commands for AWS services.
{: .fs-6 .fw-300 }

---

## Setup AWS

The minimal setup to get started using AWS services is:
1. Create an AWS root user
2. Create an AWS user
3. Add the newly created AWS user to a set of scoped permissions

### Create an AWS Root User

The AWS root user is an admin account with superuser priveleges (complete access to all
AWS services and resources in the account). Follow these
[steps from AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html) to
create such an account.

### Create an AWS User

Instead of using the AWS root user for all purposes, it's safer to follow a model of
least privelege and create a user with specific permissions. This is the AWS user.

1. [Enable IAM Identity Center](https://docs.aws.amazon.com/singlesignon/latest/userguide/get-started-enable-identity-center.html)
  * Let AWS create an AWS organization unless you're creating a user for an organization you work with.
  * Let AWS use Identity Center Directory as the identity source so you can manage users and permission groups from IAM Identity Center.
2. Create admin and power user permission sets
  * Go to IAM Identity Center > Permission sets
  * Create a permission set using a predefined permission set of "AdministratorAccess"
  * Create a permission set using a predefined permission set of "PowerUserAccess"
3. [Create a user in IAM Identity Center](https://docs.aws.amazon.com/singlesignon/latest/userguide/addusers.html)
4. Assign the permission groups to the user
  * Go to IAM Identity Center > AWS accounts
  * Check the box next to the account you created and select 'Assign Users or Groups'
  * Go to the users tab and assign the username you created and click Next
  * Select both permission sets you created (AdministratorAccess and PowerUserAccess), click Next, then Submit