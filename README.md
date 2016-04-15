# StelligentProject
# Automation for the people documentation

The below documentation describes the CloudFormation template attached with this documentation. The template is meant to be hassle free and display "Automation for the people" text after launch.

The template is designed to test both integrity of the file and if a web server is launched correctly.

## Template walkthrough

The CloudFormation template shall be in JSON format and using Template Anatomy(https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html).



The first notions such as **AWSTemplateFormatVersion** are optional and used for description of the template. It can be treated as a template metadata.

>>>> Mappings section is not strictly AWS CloudFormation related as it describes variables referenced in different parts of the template. 

>>>> The **AWSRegionArch2AMI** mapping is matching chosen AWS region to EC2 AMI (system image).

____________________________________________________________________________________________________________________________________________________________________

>>>> Next section describes an instance that we'd like to launch. In current case, we want to start a web server instance which has to configure web server and default HTML page after start. 
In order to do that, we set Install config set where we define installation of the web server (packages -> yum -> httpd) and the default page (files -> index.html -> content).
In this section we also define CloudFront specific launch scripts. Those are not task related, so we'll skip describing them and move services subsection. 

>>> The services subsection describes Linux services to run including httpd service which is required for running the web server.

>>> The **Properties** subsection specifies all instance specific properties such as base image ID, instance type, default security groups (described below) 
and a launch script which signals to the CloudFront that the web server is up and running. The signal timeout is defined in **CreationPolicy** subsection and is set to 5 minutes.

>>> The **WebServerSecurityGroup** section describes default port access which is set to open for ports 22 (SSH) and 80 (HTTP).For the purpose of this excercise, a Keypair wasn't created to SSH into the machine.

>>> The last section of the template defines required output which is an URL of the launched instance. By accessing the URL we should see the "Automation for the people" header.


_____________________________________________________________________________________________________________________________________________________________________

## Launching template & Testing Infrastructure

The template can be launched using AWS Management Console(https://console.aws.amazon.com/cloudformation/home) or by using AWS CLI. The former method is easier to use as it's done using GUI 
and a validation of the template is done automatically in a launch process.

Format of URL looks like this:

https://console.aws.amazon.com/cloudformation/home?region= **region**#/stacks/new?stackName= **stackName**&templateURL= **templateURL**


The template is stored in an S3 bucket which is accessible. 

1. Please copy the url below and launch in your browser: 
 
https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=AutomationForThePeopleStack&templateURL=https://s3.amazonaws.com/stelligentproject/automation-for-the-people.template

2. Login in to your AWS account and this should be creating your infrastructure.

1. Go to the CloudFormation page and wait till the your new stack with the name AutomationForThePeopleStatck staus changes to CREATE_COMPLETE.


## Verifying if this exercise was a success

1. Go to the output tab

2. Under Value tab, click on the URL which should read something like: http://ec2<IP-ADRESS OF WEBSERVER>.compute-1.amazonaws.com

3. This should open a web-page displaying: Automation for the people.

________________________________________________________________________________________________________________________________________________________________________________

Thank you for taking the time to review...............


Eric Adjei-Boampong.

571 533 8486.



