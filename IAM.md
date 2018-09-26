# IAM
IAM or Identity Access Management is used by AWS to create user, groups and roles.

The IAM service is global meaing it has no region.

AWS creates a root account when you first create your AWS account. The root account should only be used when needed and not day to day.

You can enable two factor authentication on all accounts created within IAM and as standard it should be. It is very important that this is done on the root account.

When creating user accounts, users can access AWS in two ways. Either via the console or the API/command line tool set. If accessing via the API/command line you will need the access key ID and secret access key which are created at user creation. If you forget these you will need to re-issue them, however the original keys will no longer work.

Roles are used to give permissions to entities that you trust. An entitiy can be either a user or another AWS service.

Roles are made up of policies which are even defined by the user or by the ones created by AWS. Policy documents are in JSON format. Two policies which seem similar are the AdministratorAccess and SystemAdministrator policy. There are however differences between the two. AdministratorAccess is the same level as the root account whereas the SystemAdministrator role is more defined:

AdministratorAccess:
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "*",
            "Resource": "*"
        }
    ]
}
```
SystemAdministrator (list has been shortend):
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "acm:Describe*",
                "acm:Get*",
                "acm:List*",
                "acm:Request*",
                "acm:Resend*",
                ...
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "ec2:AcceptVpcPeeringConnection",
                "ec2:AttachClassicLinkVpc",
                "ec2:AttachVolume",
                "ec2:AuthorizeSecurityGroupEgress",
                "ec2:AuthorizeSecurityGroupIngress",
                ...
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": "s3:*",
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "iam:GetAccessKeyLastUsed",
                "iam:GetGroup*",
                "iam:GetInstanceProfile",
                "iam:GetLoginProfile",
                "iam:GetOpenIDConnectProvider",
                ...
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "iam:GetRole",
                "iam:ListRoles",
                "iam:PassRole"
            ],
            "Resource": [
                "arn:aws:iam::*:role/rds-monitoring-role",
                "arn:aws:iam::*:role/ec2-sysadmin-*",
                "arn:aws:iam::*:role/ecr-sysadmin-*",
                "arn:aws:iam::*:role/lamdba-sysadmin-*",
                "arn:aws:iam::*:role/lambda-sysadmin-*"
            ]
        }
    ]
}
```

You can also change the sign in link for the console within IAM.