# gha-aws-ssm-get-parameter

Get a parameter from AWS SSM and store it on the system.

## Usage

```yml
jobs:
  get-parameter:
    permissions:
      contents: read
      # required to make OIDC work
      id-token: write
    
    steps:
      - uses: thebrowsercompany/gha-aws-ssm-get-parameter
        with:
          aws-role-to-assume: ${{ secrets.AWS_ROLE }}
          aws-role-session-name: ${{ env.AWS_ROLE_SESSION_NAME }}
          ssm-parameter: ${{ env.AWS_SSM_PARAMETER }}
          save-to-filepath: ${{ github.workspace }}/aws-ssm-parameter.txt
          save-to-env-var: AWS_SSM_PARAMETER
```

## Inputs

```yml
aws-role-to-assume:
  description: The AWS Role to assume.
  required: true
aws-role-session-name:
  description: A name to associate with this AWS access for auditing purposes.
  required: true
aws-region:
  description: The AWS region to use.
  required: false
  default: 'us-east-2'
aws-ssm-parameter:
  description: The path to the value in the SSM store.
  required: true
save-to-env-var:
  description: Store the parameter value in the environment variable with this name.
  required: false
save-to-filepath:
  description: Store the parameter value in the file at this path. The caller must remove this at the end.
  required: false
```

## Limitations

### Platform Support

- [x] Windows
- [ ] MacOS
- [ ] Linux