# IAM

- IAM is a Global Service.
- Permissions are defined in JSON documents named **policies**
- Always apply least privilege principle
- Users in groups heredite the permissions from the group

## Policies structure
- Version: policy language version, always include “2012-10-17”
- Id: an identifier for the policy (optional)
- Statement: one or more individual statements (required)

Statements consists of:
- Sid: an identifier for the statement (optional)
- Effect: whether the statement allows or denies access (Allow, Deny)
- Principal: account/user/role to which this policy applied to
- Action: list of actions this policy allows or denies
- Resource: list of resources to which the actions applied to
- Condition: conditions for when this policy is in effect (optional)


## AWS STS - Security Token Service

- Allows to grant limited and temporary access to AWS resources
- Token valid for up to one hour (must be refreshed)
- STS most important APIs:
    - **AssumeRole**:
        - Usage within our account: for temporary enhanced security
        - Cross account: assume role on target account to perform actions there
    - **AssumeRoleWithSAML**:
        - Return credentials for user logging in with SAML
    - **AssumeRoleWithWebIdentity**:
        - Return credentials for users logged in with IdP (Facebook login, Google login, OIDC)
        - AWS recommends against using this, use Cognito instead
    - **GetSessionToken**:
        - Fro MFA, from an user or AWS account root user

## Using STS to Assume a Role

1. Define an IAM Role within an account or cross-account
2. Define which principals can access this IAM Role
3. Use AWS STS to retrieve credentials and impersonate the IAM Role you have access to (AssumeRole API)
4. Temporary credentials will be valid for 15 minutes up to 1 hour
