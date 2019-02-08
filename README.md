What's Here
-----------

This sample includes:

* README.md - this file
* app.js - this file contains the code for your application
* appspec.yml - this file is used by AWS CodeDeploy when deploying the web
  application to EC2
* package.json - this file contains various metadata relevant to your Node.js
  application such as dependencies
* public/ - this directory contains static web assets used by your application
* scripts/ - this directory contains scripts used by AWS CodeDeploy when
  installing and deploying your application on the Amazon EC2 instance

Your Lab Instructions
---------------

To run this code locally, you'll need to clone your project's repository to your
local computer. **NOTE** not a required step to complete the lab.

1. Install NPM dependencies:

        $ npm install

2. Start the development server:

        $ node app.js

3. Open http://localhost:3000/ in a web browser to view your application.


**CodeDeploy Lab:**

* Create an IAM role for CodeDeploy (role that has correct permissions for CodeDeploy)
  * Instructions: https://docs.aws.amazon.com/codedeploy/latest/userguide/getting-started-create-service-role.html#getting-started-create-service-role-console

* Create an IAM instance profile (Policy and Role to manage EC2 instances for the deploy)
  * Instuctions: INGORE NOTE ON STEP 3: https://docs.aws.amazon.com/codedeploy/latest/userguide/getting-started-create-iam-instance-profile.html#getting-started-create-iam-instance-profile-console

* Create an EC2 Instance that will host your application
  * **IMPORTANT** Use **ami-0cd3dfa4e37921605**, choose an exisiting VPC that you have used for a previous lab that has worked for you in the past, and when given the option for **auto-assign** public ip choose enable, Make sure on the security group page you add HTTP as an inbound rule with the default ssh rule.
  * Code for user data to install CodeDeploy Agent:

                #!/bin/bash
                yum -y update
                yum install -y ruby
                cd /home/ec2-user
                curl -O https://aws-codedeploy-us-east-2.s3.amazonaws.com/latest/install
                chmod +x ./install
                ./install auto

  * Instructions (consider the above notes when following the guide): https://docs.aws.amazon.com/codedeploy/latest/userguide/instances-ec2-create.html

  * Verify that the agent is running (you will need to ssh to the machine):
    * https://docs.aws.amazon.com/codedeploy/latest/userguide/codedeploy-agent-operations-verify.html#codedeploy-agent-operations-verify-linux

  * Create application and deployment group (this is what will deploy to your EC2 instances with the tags that match the deployment group)
    * Instructions (skip step 14 and 15): https://docs.aws.amazon.com/codedeploy/latest/userguide/tutorials-github-create-application.html








