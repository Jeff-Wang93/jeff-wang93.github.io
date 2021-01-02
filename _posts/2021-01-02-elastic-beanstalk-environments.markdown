---
layout: default
title:  Multiple Elastic Beanstalk Environments Setup
date:   2021-01-02
categories: aws web development ec2 elastic-beanstalk
---
Everyone's doing a shift (or has already done) towards cloud/serverless
computing. It's just much less of a hassle when you're running software of any
kind. You don't have to worry about infrastructure or scaling. Everything is
magically done for you.

## What's the point of this post?
Speaking of which, this short post is going to be around AWS Elastic Beanstalk
(EB) and how we can set up different environments. If you aren't familiar with 
EB, it's basically an interface to an EC2 instance. It provides a lot of in the 
box functionality, like autoscaling and other configurations. In addition, 
there's no additional cost to using EB; Just pay for the services that EB is managing. 

I would say it's rather common for teams to have multiple environments for their
application. For example, these environments could be development versions, 
testing versions, and production versions. 

In addition, it's also common for applications to have `.env` files. These files
are mainly used to hold sensitive information (eg: API keys, passwords, etc.)
that should not be viewable/available in their code repos. Naturally, the
different environments should also have their own respective `.env` files. 

So how do we set it up such that we can have different EB environments with
different `.env` files if we can't commit the `.env` files? 

## What do we do?
It's pretty simple. EB provides some tools we can leverage to achieve this.

Let's assume our `.env` files are in some AWS S3 bucket. We need to pull the
file before the application builds. If we don't, our application will fail to
build because there's going to be environment variables that can't be resolved.
Beanstalk
In your project root, create an folder called `.ebextensions`. This will house
files that will give commands to EB. In the folder, create a file called
`YOUR_NAME.config` where `YOUR_NAME` is a name of your choice.

In that file, have the following:
```
container_commands:
    00_download_env_file:
        command: aws s3 cp $ENV_FILE .env
```

As you can see, we're going to use the AWS CLI to interface with S3 and pull the
file we desire. `$ENV_FILE` is the S3 URI of the appropriate file. We need to
resolve this variable ourselves. To do so, open the EB console (aka the web
interface).

![](/images/2021-01-02-elastic-beanstalk-environments/eb-env-variables.PNG)

Scroll to the bottom and you should see something like the image below:

![](/images/2021-01-02-elastic-beanstalk-environments/eb-sidebar.png)

Click `Edit` and input $ENV_FILE as the key and the S3 URI that you wish to 
use as the value and click apply

And you're done. That was pretty simple right? Now, every time EB
restarts/builds the app, it will first pull the file from S3.

## What if I got errors?
If you encounter errors with this, you can view the logs in the EB instance and
that should tell you what went wrong.

To view the logs, SSH into your EB instance. 

The exact file is `/var/log/cfn-init-cmd.log`. In that file, you'll see any
errors regarding the command.
