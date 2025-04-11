# F-to-F Bill Uploader

## Overview

The **F-to-F Bill Uploader** is a Node.js application designed to upload bill information to a DynamoDB table and log output details to AWS CloudWatch. The application lets you enter bill parameters directly via the command line, making it easy to add new bills to your system.

In this project, a bill is uploaded with a single command. For example:

`npm start "affirm" "38" "8th"`
In this command:

`"affirm"` represents a label or identifier for the bill.

`"38"` could represent a bill amount or another numeric value.

`"8th"` is used to indicate the due day for the bill (this value is used to calculate the full due date).

## How It Works
Parsing Command Line Arguments:

The application accepts the bill details from the command line.

It processes these arguments to create a bill object that includes the provided data and a computed full due date, based on today’s date.

### Uploading to DynamoDB:

After processing the bill data, the application uploads the bill as an entry in the DynamoDB table named Bills.

The table entry includes the user-provided fields, along with a computed property (like fullDueDate) determined by the due day.

### Logging to CloudWatch:

Output including processing details and any errors are logged to AWS CloudWatch.

This makes it easier to monitor the application’s behavior, review the full bill data entries, and troubleshoot if needed.

## Running the Application

**Step 1:** Prepare Your Environment

- AWS Credentials:
Ensure your AWS credentials are configured (via environment variables, AWS CLI configuration file, etc.) so that the AWS SDK can access DynamoDB and CloudWatch.

- DynamoDB Table:
Verify that you have a DynamoDB table named Bills in your AWS account. This table should be structured to accept bill entries that include a due day value.


**Step 2:** Run the Command to Upload a Bill
In your project folder, open your terminal and run:

bash
Copy
`npm start "affirm" "38" "8th"`
This command will:

Parse the provided arguments.

Compute the full due date based on today’s date and the provided due day.

Upload the bill data to the DynamoDB table.

Log all important outputs (including the computed date, the list of bills, and any error messages) to CloudWatch.



**Step 3:** Verify on AWS
- **DynamoDB**
Check the Table:

Log in to the AWS Management Console.

Navigate to DynamoDB and open your Bills table.

Review the items in the table. You should see an entry corresponding to the bill you just uploaded with the new computed fullDueDate.

- **CloudWatch**
Review Logs:

In the AWS Management Console, go to CloudWatch.

Click on Logs in the side menu.

Locate the log group associated with the application (this could be named after your Lambda function or specified in your project’s configuration).

Open the most recent log stream to view the detailed output logged by the application. Here you should see the console logs of the current date, the processed bill data, and any other debugging information.
