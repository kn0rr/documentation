# IAM

## IAM Policies Structure

The JSON-Structure for IAM policies consists of:
- Version: Policy language version, alwasy include "2012-10-17"
- Id: an identifier for the policy (Optional)
- Statement: one or more indivudal statements (required), which consists of
    - Sid: an identifier for the statement (optional)
    - Effect: Wheter the statement allows or denies access (Allow, Deny)
    - Prinicipal: account/user/role to which this policy applies to
    - Actions: List of actions this policy allows or denies
    - Resource: list of resources to hich the actions applies to
    - Condition: conditions for when this policy is in effect (optional| not reflected in the statement below) 

````json
{
    "Version": "2012-10-17",
    "Id": "S3-Account-Permissions", // Optional
    "Statement": [
        {
            "Sid": "1", //Optional
            "Effect": "Allow",
            "Principial":{
                "Aws":["arn:aws:iam::123456789012:root"]
            },
            "Action":[
                "s3:GetObject",
                "s3:PutObject"
            ],
            "Resource":["arn:aws:s3:::mybucket/*"]
        }
    ]
}

````