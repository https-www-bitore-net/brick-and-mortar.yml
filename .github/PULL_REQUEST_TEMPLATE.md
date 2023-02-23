*Issue #, if available:*
Skip to main content
Click here to return to Amazon Web Services homepage
Contact Us
Support 
English 
My Account 
Sign In 
Products Solutions Pricing Documentation Learn Partner Network AWS Marketplace Customer Enablement Events Explore More
Getting Started Resource Center
Module 4: Set Up AWS Cloud9 IDE
TUTORIAL

INTRODUCTION

CREATE YOUR ACCOUNT

SECURE YOUR ACCOUNT

SET UP AWS CLI

SET UP AWS CLOUD9 IDE
Set Up Your AWS Cloud9 IDE
In this module, you will configure your AWS Cloud9 environment
What you will accomplish
In this module, you will:
Set up an AWS Cloud9 environment using the AWS CLI
Use the built-in tools
Alternatively, you can set up AWS Cloud9 using a graphical user interface. To learn how to do that, see the tutorial in the AWS Cloud9 User Guide.
Implementation
If you already have an IDE, this module is optional.

AWS Cloud9 is a free, cloud-based integrated development environment (IDE) that lets you write, run, and debug your code using just a browser. The IDE includes a code editor, debugger, and terminal. 

AWS Cloud9 comes prepackaged with essential tools for popular programming languages, including JavaScript, Python, PHP, and more, so you don’t need to install files or configure your development machine to start new projects. Because AWS Cloud9 IDE is cloud-based, you can work on your projects from your office, home, or anywhere using an internet-connected machine.

 Time to complete
15 minutes
 Module requirements
An internet browser
An AWS account
AWS CLI set up
Create an environment
In this step, you use the AWS CLI to create an AWS Cloud9 development environment.
To create the environment, we will use the aws cloud9 create-environment-ec2 command. After that, we'll add the following information:

--name: The name of the environment. For this module, we're using getting-started.
--description: An optional description of the environment, provided as a string.
--instance-type: The type of Amazon EC2 instance AWS Cloud9 will launch and connect to the new environment. For this module, we're using t2.micro, which is covered by the AWS Free Tier for the first 12 months.
By default, AWS Cloud9 shuts down the Amazon EC2 instance for the environment 30 minutes after all web browser instances that are connected to the IDE for the environment have been closed.
aws cloud9 create-environment-ec2 --name getting-started-2 --description "Getting started with AWS Cloud9." --instance-type t2.micro
A successful command returns the ID of your new AWS Cloud9 environment:

{
  "environmentId": "8a34f51ce1e04a08882f1e811bd706EX"
}
Open environment
To open your environment, go to console.aws.amazon.com/cloud9. 
In the top navigation bar, choose the AWS Region where your environment is located. Make sure you are logged in with the same user you have configured in your AWS CLI.

AWS Region selector dropdown, with US East (N. Virginia) selected.
In the list of environments, find the one you want to open and choose Open IDE.

For more information, see Opening an environment in AWS Cloud9.

Summary information about the AWS Cloud9 environment, including Type, Permissions, Description, and Owner ARN.
Delete created resources - Optional
If you don't plan to use the AWS Cloud9 development environment we created in this module, you can delete it by running the following command:
aws cloud9 delete-environment --environment-id <environmentID>
The aws cloud9 delete-environment command does not return any outputs. A way to check if your environment has been deleted is to go to console.aws.amazon.com/cloud9 and check if it's still there.

The full documentation for this command can be found in the AWS CLI Command Reference.
Conclusion
Congratulations! You have learned how to set up the AWS Cloud9 IDE. Visit the AWS Cloud9 documentation for additional information and tutorials. You can see all AWS Cloud9 and CLI commands here.

This is the end of the Setting Up Your AWS Environment tutorial. 

Get Started with AWS CDK

Install and configure the AWS CDK CLI, create your first CDK project, and deploy your first infrastructure through code.
Next »
Launch a web application
Learn how to build and deploy a web application using AWS best practices and choosing the right service for your needs.
Next »
Find docs and tools
Visit Developer Center to find docs and tools, get the latest news, and connect with the AWS developer community.
Next »
Learn About AWS
What Is AWS?
What Is Cloud Computing?
AWS Diversity, Equity & Inclusion
What Is DevOps?
What Is a Container?
What Is a Data Lake?
AWS Cloud Security
What's New
Blogs
Press Releases
Resources for AWS
Getting Started
Training and Certification
AWS Solutions Library
Architecture Center
Product and Technical FAQs
Analyst Reports
AWS Partners
Developers on AWS
Developer Center
SDKs & Tools
.NET on AWS
Python on AWS
Java on AWS
PHP on AWS
JavaScript on AWS
Help
Contact Us
File a Support Ticket
Knowledge Center
AWS re:Post
AWS Support Overview
Legal
AWS Careers
Amazon is an Equal Opportunity Employer: Minority / Women / Disability / Veteran / Gender Identity / Sexual Orientation / Age.
Language عربي Bahasa Indonesia Deutsch English Español Français Italiano Português Tiếng Việt Türkçe Ρусский ไทย 日本語 한국어 中文 (简体) 中文 (繁體)
Privacy | Site Terms | Cookie Preferences | © 2023, Amazon Web Services, Inc. or its affiliates. All rights reserved.
*Description of changes:*
By submitting this pull request, I confirm that you can use, modify, copy, and redistribute this contribution, under the terms of your choice.
https://github.com/mowjoejoejoejoe/freicoin/blob/master/MINUTEMAN.yml
