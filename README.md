# Secret Store SQS Worker Lambda

**NOTE: Rosa (www.rosa.bot) is the new name for ForgotPW**

Process events to store secrets.  When requests are submitted from the REST API to store secrets such as password hints, an SNS event is fired.  An SQS queue created in this project subscribes to these events and this worker processes these SQS messages.  Secrets are stored in an encrypted S3 bucket.

## Setup

Install the Serverless CLI.

```shell
# install the serverless framework
npm install serverless -g
```

## Deploy

```shell
export AWS_ENV="dev" && export PROFILE="fpw$AWS_ENV"
iam-starter --profile $PROFILE --command sls deploy --verbose
```

## Invoke Locally

```shell
# ensure we are matching the version of node used by lambda
nvm use 8.10.0
export AWS_ENV="dev" && export PROFILE="fpw$AWS_ENV"

# pip install iam-starter
iam-starter \
    --role role-ops-devops \
    --profile $PROFILE \
    --command sls invoke local \
    -f fpw-secret-store-sqsworker \
    -p ./events/ValidStoreSQSRequest.json \
    -l
```

# License

GNU General Public License v3.0

See [LICENSE](LICENSE.txt) to see the full text.
