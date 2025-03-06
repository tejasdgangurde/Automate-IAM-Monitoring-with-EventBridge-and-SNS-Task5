# Automate-IAM-Monitoring-with-EventBridge-and-SNS
This guide will walk you through setting up Amazon EventBridge to trigger an SNS notification whenever a new IAM user is created.
________________________________________________________________________________________________________________________________________________________________
Step 1: Create an SNS Topic for Notifications
Amazon Simple Notification Service (SNS) will be used to send notifications when a new IAM user is created.
1.1 Create an SNS Topic
1.	Sign in to the AWS Management Console.
2.	Open the Amazon SNS console: SNS Console.
3.	In the left menu, click Topics.
4.	Click Create topic.
5.	Choose Standard as the type.
6.	Enter a Topic name (e.g., IAMUserCreationAlerts).
7.	Click Create topic.
1.2 Create an SNS Subscription
1.	Open the newly created SNS topic.
2.	Click Create subscription.
3.	Select Protocol (choose Email or SMS, depending on your preference).
4.	Enter the Endpoint (e.g., an email address for notifications).
5.	Click Create subscription.
6.	Check your email and confirm the subscription.
________________________________________________________________________________________________________________________________________________________________
Step 2: Create an EventBridge Rule
Amazon EventBridge will monitor IAM events and trigger the SNS notification.
2.1 Open EventBridge Console
1.	Open the Amazon EventBridge console: EventBridge Console.
2.	In the left menu, click Rules.
3.	Click Create rule.
2.2 Configure the Rule
1.	Rule name: Enter IAMUserCreationRule.
2.	Event bus: Select default.
3.	Rule type: Select Rule with an event pattern.
2.3 Define the Event Pattern
1.	Choose Event source: AWS services.
2.	Choose Service name: IAM (Identity and Access Management).
3.	Choose Event type: AWS API Call via CloudTrail.
4.	Click Edit pattern (JSON) and enter the following JSON to capture IAM user creation events:
json
CopyEdit
{
  "source": ["aws.iam"],
  "detail-type": ["AWS API Call via CloudTrail"],
  "detail": {
    "eventSource": ["iam.amazonaws.com"],
    "eventName": ["CreateUser"]
  }
}
5.	Click Next.
________________________________________________________________________________________________________________________________________________________________
Step 3: Set Target as SNS
1.	Select target type: AWS service.
2.	Choose a target: SNS topic.
3.	Select SNS topic: Choose the IAMUserCreationAlerts SNS topic you created earlier.
4.	Click Next.
________________________________________________________________________________________________________________________________________________________________
Step 4: Review and Create the Rule
1.	Review the settings.
2.	Click Create rule.
________________________________________________________________________________________________________________________________________________________________
Step 5: Test the Setup
1.	Open the IAM Console: IAM Console.
2.	Create a new IAM user.
3.	Check your email (or SNS subscriber) for a notification.
________________________________________________________________________________________________________________________________________________________________
