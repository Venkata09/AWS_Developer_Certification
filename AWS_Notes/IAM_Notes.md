##IAM

Roles

is a iam entity which defines set of permissions for making aws service requests
Roles allow someone or a set of code or instance to assume certain permissions- More secure than using api codes
users, ec2 or even web identity can assume roles
Identity federated login like facebook etc . Federated login can assume a role- policy can be attached to user to give it privileges. the api credentials can then be used to login from anywhere and get the privileges
no limit on number of roles you can assume
you can create 250 IAM roles under your aws account. more can be added by contacting AWS
you cannot change the role of a running EC2 instance
Only one role can be attached to an EC2 instance
If a role is deleted then the ec2 instance tied to the role will lose permissions immediately
Groups

Collection of IAM users, users can be added or removed from any group
User can belong to multiple groups
Group cannot belong to another group
Groups can be granted access control policies
groups do not have security credentials, so groups cannot login. they are only for managing users
role cannot be added to a group
users can be structured in hierarchical way like ldap

users are global entity and are not bound to regions

multiple mfa devices can be procured and then assigned to users

user access keys and x.509 certificates can be rotated

users cannot have individual ssh keys for ec2. there is one ssh key per ec2 instance

iam users need not have email address

password policy can be set for passwords

No quotas can be set on a per user basis

The AWS sign-in endpoint for SAML is https://signin.aws.amazon.com/saml

The default region for an SDK is "US-EAST-1"

temporary security credentials : min 1 hour, default 12 and max 36 hours validity

Common API

AssumeRole, AssumeRoleWithWebIdentity, and AssumeRoleWithSAML
GetFederationToken
