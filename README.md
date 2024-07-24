# Trigger Slack Webhook

## Overview
This repository contains Salesforce Apex code designed to facilitate the sending of messages from Salesforce to Slack using Slack Webhooks. The integration is encapsulated into two main components: an Apex Class (`TriggerSlackWebhook`) and its corresponding test class (`TriggerSlackWebhookTest`).

## Components

### Apex Class: TriggerSlackWebhook
The `TriggerSlackWebhook` class is designed to be used as a callable method within Salesforce that interacts with Slack via HTTP callouts. It is equipped to handle multiple requests simultaneously, each potentially targeting different Slack channels or messages.

#### Features
- **Invocable Method**: The `sendToSlack` method can be invoked from Salesforce flows or processes, making it easy to integrate with various business workflows.
- **Customizable Message Sending**: The method accepts a list of requests, where each request includes the Slack webhook URL, the message content, the Salesforce record ID, and optionally, the Slack channel name.

#### Method Details
- `sendToSlack(List<Request> requests)`: Processes each request to send a message to the specified Slack webhook endpoint. The message payload is formatted as JSON to meet Slack's requirements.

### Apex Test Class: TriggerSlackWebhookTest
The test class `TriggerSlackWebhookTest` ensures the functionality of `TriggerSlackWebhook` via unit tests. It uses mock callouts to simulate interactions with Slack, verifying both the request payload and the behavior of the `sendToSlack` method under various conditions.

#### Test Features
- **HttpCalloutMock Implementation**: Simulates Slack's API to validate the integration without making real HTTP requests.
- **Response Validation**: Ensures that the message formation and endpoint configuration are correct.

## Integration with Slack
To integrate Salesforce with Slack:
1. **Configure Webhooks in Slack**: Set up incoming webhooks in your Slack workspace to generate endpoints that Salesforce can post messages to.
2. **Set Up the Apex Class**: Deploy `TriggerSlackWebhook` in your Salesforce org.
3. **Invoke from a Salesforce Process**: Use Flow Builder or another automated method to invoke `sendToSlack` based on specific triggers within Salesforce.

## Usage
To send a message to Slack, create an instance of `Request`, populate it with necessary details such as the webhook URL, message, and record ID, and pass it to `sendToSlack`.

Example:
```java
TriggerSlackWebhook.Request myRequest = new TriggerSlackWebhook.Request();
myRequest.endpoint = 'https://hooks.slack.com/services/TXXXX/BXXXX/XXXX';
myRequest.message = 'Hello, Salesforce!';
myRequest.recordId = '001xx000003DHPx';
TriggerSlackWebhook.sendToSlack(new List<TriggerSlackWebhook.Request>{ myRequest });
