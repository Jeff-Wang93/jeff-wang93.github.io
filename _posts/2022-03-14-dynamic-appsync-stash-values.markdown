---
layout: default
title:  Detailing an Annoying Issue Regarding CloudFormation and Appsync
date:   2021-11-28
categories: aws web development cloud troubleshooting
---
## CloudFormation Hates Dynamic Naming
CloudFormation really wasn't made with dynamic elements in mind. There's a lot of workaround that you need to
do to help support dynamic elements. Here was a use case that I encountered:

We had two different AWS "environments" in a single account. We were also using Contentful to help manage
our data. With that, we had two different spaces and environments within Contentful for both sandbox and
stage. With this, it raised the issue of "how does a single AppSync resolver switch between two different 
Contentful spaces/environments?" 

## Code Within the Template
Our `Before Mapping Template` is where we can achieve what we desire. Here's what it looked like in the end:
```
RequestMappingTemplate:
        !Join
        - ''
        - - '{'
          - !If [ isProduction '$util.qr($ctx.stash.put("ContentfulUrl", "/spaces/prod/environments/prod"))', !If [ isStage, '$util.qr($ctx.stash.put("ContentfulUrl", "/spaces/stage/environments/stage"))', '$util.qr($ctx.stash.put("ContentfulUrl", "/spaces/sandbox/environments/sandbox"))' ] ]
          - ' '
          - '}'
```
Here, `isProduction` is just a CloudFormation variable that determines if we're trying to deploy a prod instance.
Of course, we have to have the logic here because only in the CloudFormation template can we have substitutions and
conditional logic.

With this, the following functions are able to access the stash and pull out the correct Contentful information.