---
layout: default
title:  Detailing an Annoying Issue Regarding CloudFormation and Appsync
date:   2021-01-03
categories: aws web development cloud troubleshooting
---
## CloudFormation is both a gift and a curse
I love and hate CloudFormation at the same time. This software has saved me
countless hours and also cost me countless hours. The main issue I have with CloudFormation is that
it doesn't have good error messages. I've experienced this countless times, especially when I was trying to
get an AppSync application running. Here's some of the errors I've encountered and how I got around
them.

## CloudFormation doesn't like renaming
For the love of god, don't rename your resolvers. CloudFormation will throw
errors and it'll take a bit to figure out why. All you'll see is this dreaded error:
```
only one resolver is allowed per field
```
The amount of time I spent looking at this was silly. I really didn't understand at the time why
this error was occuring. As it turns out, CloudFormation doesn't delete the old resource first.
It'll try to add the newly named resolver first and see that it already exists.

Here are the four steps needed to rename a resolver:
1. Delete the resolver you are trying to rename
2. Update your CloudFormation stack
3. Add the resolver with its new name
4. Update your CloudFormation stack

With this, your resolver will be successfully renamed, and everything should be working as expected.
I don't really understand why CloudFormation works in this fashion, but who am I to question the
great minds at AWS?

Hopefully this will help anyone who comes across this issue as well. 
