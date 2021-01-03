---
layout: default
title:  General Overview for Creating an AWS API for a Web App's Backend
date:   2021-01-03
categories: aws web development
---
## Why have a API centered backend?
APIs are all the rage and for good reason. When designing a web app, it makes
sense to have the backend be powered by an API. This way, you're not limited to
just one interface. 

For example, you could have both a browser web app and a phone app that 
utilize the same backend UI. If you had a web app that was both composed of a 
front and back end in the same app, adding another interface like
this would be more difficult. 

## What are some benefits to having a cloud supported API?
Now, with that out of the way, a good way of designing/developing an API is
utilizing serverless (aka cloud) computing. There's multiple reasons as to why
but I'll list a few that I feel like are huge advantages:

* You don't have to worry about scale. If you rapidly grow and begin making
  thousands and thousands of calls from hundreds, the cloud provider you
  utilize should be able to automatically scale your API as needed to meet
  demand and keep downtime at a minimum.

* Costs are very low. For example, if we utilize AWS Lambdas as our engine
  for running code, then the cost is practically non-existent thanks to
  AWS's very generous free tier (1 million free calls/400 hours of computing per
  month)

* Easily integrated with other services. For example, again using AWS as an
  example, it's very easy to call and use other AWS services. 

  This is the AWS service list that I have used to create an external facing
  API with a brief description (I'll go into more detail later):

  * AWS Cognito - User Management
  * AWS Lambda  - Service that actually runs the code
  * AWS API Gateway - A management tool that connects the endpoints with a web
    facing address. This basically means we tie an endpoint (eg:
    `/api/get-client-info`) with a Lambda function
  * AWS RDS/DynamoDB - SQL/NOSQL databases

## Explanation to the AWS services
As stated before, I'll now be going into a more detailed explanation as to
why/how I use the services I listed above.

### AWS Cognito 
Cognito is a management system that handles users, logins, registration,
etc. It's nice to use Cognito because you don't have to worry about things like
storing passwords securely, dealing with registration, dealing with forgotten
passwords, enforcing password constraints, emailing users with temporary
credentials, etc. I secure my API endpoints behind Cognito. Using the Cognito
API, I can take in a username and password and authenticate it via Cognito. If
Cognito returns true, then I can safely let the user access the API endpoint. 

In addition, Cognito can return JWT access tokens if you wish. For a web app,
when the user logs in, Cognito will return an access token, an identity token,
and a refresh token to me. I then store those three tokens as session data for
that particular user. Any time the user does an action (eg: get clients), I use
those tokens to as authentication to the API.

### AWS Lambda
Lambdas are the meat of the API. They're what's actually running the code. For
example, if I had a simple function that returned a user like so:
```
def get_user(username): 
    user = database_lookup(username)

    if user:
        return user
    else:
        return error
```
This code would be the Lambda itself. It's what's running our code.

### API Gateway
API Gateway is kind of like the connecting component between the execution of
code/functions and the client interface. 

For example, let's say we wanted an endpoint called `/api/user/get-user` to be
linked to the lambda that we wrote above. That's where API gateway comes in. 

API Gateway will generate a host url for us (eg:
`example.execute-api.us-west-2.amazonaws.com`) that we can use. Now, if we
wanted to hit our `get-user` endpoint, the full URL would be something like
this:
```
example.execute-api.us-west-2.amazonaws.com/api/user/get-user
```

API Gateway also deals with authentication/security of the endpoints. If we
wanted to have the endpoint secured with an access token, we can utilize API
Gateway to do that for us. Since I mentioned Cognito above, API Gateway has
pre-built authorizers that use Cognito tokens as Bearer tokens. If you don't use
Cognito or simply wish for your own custom authorizer, you can write your own
Lambda and have API Gateway lock the endpoint behind that custom Lambda.
Overall, a very powerful service.

I won't really go into detail with RDS/DynamoDB since they're just databases.

As you can see, using AWS services, it's quite simple to design/create your own
cloud backed API. As mentioned before, with AWS, it's easy to integrate the
different components together. Most of the integration is built in so you just
have to do a little clicking in the AWS interface to link the different
services.

## What if I don't want to use cloud infrastructure?
There's plenty of reasons as to why someone would choose to not use cloud
infrastructure. One reason could be that the work they're doing would violate
the TOS set by AWS. Another reason could also be that using an external service
would create a security issue.

If you still wanted an API, you would have to pretty much do everything manually
but it's not that bad honestly. 

For example, say we wanted an API, and our language of choice is Python. Then I
would probably recommend [Flask](https://flask.palletsprojects.com/en/1.1.x/).
Then, it's just utilizing the framework to do what you need it to do. I'll
probably go into more detail in a later post as to how to do that.
