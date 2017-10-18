 IAM Essentials

IAM is global to all AWS regions (creating a user account will apply to all the regions)
Practice the “Principle of Least Privilege” when administering AWS accounts, users, groups, and roles.

IAM Policies

By default an explicit deny always overrides an explicit allow
IAM provides pre-built policy templates (currently 265), examples:
- Administrator access: Full access to ALL AWS resources
- Power user access: Admin Access except user/group management
- Read only access

IAM Users

User ARN = User Amazon Resource Name
Users credentials should NEVER be stored or “passed” to an EC2 instance

IAM Groups

Allows for easier access management to AWS resources

IAM Roles

Roles must be used because policies cannot be directly attached to AWS services.
An EC2 instance can only have ONE role attached at a time (e.g. access to S3).
“Identity Provider Access” role: a “role” for access to AWS Accounts and Resources through Active Directory, SSO, or similar.

IAM API Keys

API Access Keys are required to make programmatic calls to AWS from the:
- AWS CLI
- Tools for PowerShell
- AWS SDKs
- Direct HTTP API calls

API Access Key Facts:
- Only available ONE time (user creation OR reissue a new set of keys)
- After creation, you can only see the Access Key ID (never the Secret Key ID)
- NEVER create or store API keys on an EC2 instance

IAM Quiz

Note: T = True statement.

T: If an IAM access policy has both an allow rule and a deny rule for the same service, the DENY rule will supersede the allow rule.

Q: You create a new IAM user for AUSER in you company’s AWS account. On AUSER’s first day, you ask AUSER to make a change to a Cloudwatch alarm in an Auto Scaling group. AUSER reports no access to Cloudwatch or Auto Scaling in the AWS console. What is a possible explanation for this?
A: You have not added the appropriate IAM permissions and access policies to AUSER; there is a non-explicit deny to all new users.

T: An IAM user can have many IAM permission policies attached to them at the same time, either directly attached or through groups.

Q: What best describes an IAM role?
A: A role is something that another entity can “assume”

Q: AUSER will be overseeing the company’s DynamoDB database, so you attached the “AmazonDynamoDBFullAccess” IAM policy to AUSER’s IAM user. 6 months later, AUSER was promoted to manager and added to the “Managers” IAM group. The “Managers” group does not have the “AmazonDynamoDBFullAccess” policy attached to it. What will happen to AUSER’s DynamoDB access?
A: Nothing, as an IAM user can have multiple IAM permission policies attached to them at the same time, either directly to the user or through an associated IAM group.

T: By default, when an IAM user is created, it has a non-explicit “deny” for all AWS services.

Q: What are the main benefits of IAM groups?
A: Assigning IAM permission policies to more than one user at a time.
A: Easier user/policy management.

T: Best practice is to NEVER store or pass IAM credentials to an EC2 instance.

Q: What best describes the “Principal of Least Privilege”?
A: Users should be granted permission to access only the resources they need to do their assigned job.

Q: The common use for IAM is to manage what?
A: Users, Groups, Roles, Access Policies, API Keys, Password Policies, Multi-Factor Authentication

Q: EC2 instance must have the ability to access other AWS resources. What is the best way to manage this access?
A: Use an IAM role to manage temporary credentials for applications that run on an EC2 instance. The role will supply temporary permissions that applications can use when they make calls to other AWS resources.

Q: API Access Keys are required to make programmatic calls to AWS from which of the following?
A: AWS CLI, Tools for PowerShell, AWS SDKs, Direct HTTP API calls

Q: You notice that one of the groups has two conflicting permissions attached: one that allows S3 access, and one that denies S3 access. If your goal is to allow members of the group to have S3 access, what needs to be done?
A: You must remove the deny policy, as a deny policy will override an allow policy.
