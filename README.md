# Simple Alexa Skill that interacts with ServiceNow

This Alexa Skill queries a ServiceNow instance for most recent tickets and plays them back.

## You will need...

- NodeJS and ```npm``` installed

- An AWS account. CAUTION: You will incur charges, unless you are using the free-tier. You can sign up for a free tier account [here](https://aws.amazon.com/free)

- An IAM user with appropriate roles

- An Amazon developer account. You can create one [here](https://developer.amazon.com)

- A ServiceNow developer instance. You can sign up for a developer instance [here](https://developer.servicenow.com)

- AWS CLI. Install and configure as outlined [here](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)

- ASK CLI. Install and configure as outlined [here](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html)


## How to deploy

Amend ```constants.js``` with the name of your ServiceNow instance:
```bash
exports.servicenow = {
  instance: 'devNNNNN.service-now.com',
};
```

Download the skill dependencies:
```bash
$ cd lambda/custom; npm install
```

Deploy the skill and lambda function with ASK CLI:
```bash
$ ask deploy
```

Create OAuth API Endpoint in ServiceNow. Navigate to System OAuth -> Application Registry. Create a new entry with following values:
- Name: ```Simple Alexa Skill```
- Redirect URL: ```https://layla.amazon.com/api/skill/link/M26D1D2CM95YM6```

Use the auto generated Client Id and Client Secret to Link the skill user account with ServiceNow.

- Log into Alexa developer console and navigate to the skill
- Select the Account Linking tab and enter the following details:
- Authorization URI: ```https://devNNNNN.service-now.com/oauth_auth.do```
- Access Token URI: ```https://dev21029.service-now.com/oauth_token.do```
- Client Id: ```<As generated by ServiceNow above>```
- Client Secret: ```<As generated by ServiceNow above>```

## Take it for a spin

You:  "Alexa, open ServiceNow"

Alexa: "Welcome to the ServiceNow skill. How can I help?"

You: "Tell me the recent incidents"

Alexa: "Here are the 5 most recent incidents..."

## Tidy up

Once you're done, you can clean up as follows.

- delete the lambda function (ask-custom-alexa-servicenow)
- delete the IAM execution role (ask-lambda-alexa-servicenow)
- delete the skill 
