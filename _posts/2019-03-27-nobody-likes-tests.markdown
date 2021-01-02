---
layout: default
title:  Let Testing Into Your Life
date:   2019-03-27 
categories: testing
---
# Testing and the software engineering world
Testing is like infrastructure. It's necessary. We need it. Everyone talks 
about implementing it or expanding it, but god is testing unsexy. 

# It's a love hate relationship
Though I have pretty limited experience in software engineering, it seems 
like most people, at least in my opinion, don't take testing very seriously. 
It's usually an afterthought or something people do to try and get those 
nice Github badges. It's a shame really. I feel like a lot of headaches would 
be solved had there been some sort of automatic testing in place.

# So, what is testing?
It's basically making sure your code works and does what it needs to do. Let's 
also make a distinction before I go further. I am not saying that automation is
this amazing concept that is flawless because it's not. There are many times
where manual testing makes more sense than automated testing. A good example of
where manual is preferred over automation is if the page that automation will be
written for is going to be undergoing drastic changes.  

With that said, I'll be talking about automated testing  (though manual testing
is much appreciated). So there are many major types of testing with regards to
web based programs but let's focus on these two: Unit and Front End Auotmation.

# Unit Testing
In layman terms, unit testing is a test where, using some kind of framework
like `pytest` or `junit`, you send input into some function and assert the
function worked correctly. Let's see an example using some pseudocode.

Here's a function that we want to write a unit test for:
```
function add5(x) {
    return 5 + x
}
```
Here's what a example of a test function that will send input to the function
above:
```
function add5Test() {
    varA = add5(5)
    varB = add5(10)
    assert varA == 10
    assert varb == 10
}
```
This is a relatively simple example and quite straight forward. We have some
function and we send in different inputs to that function and ensure that what 
the function returns is what we expect which is what the `assert` is doing. In 
a more real life example, the test function would try to account for many 
types of inputs. What if `add5` was given a string instead of an int? Can the 
function handle negative numbers? How about decimals? 

Clean, simple, and effect. It's great that we can ensure each function works 
individually, but, in my opinion, it's not enough. We need to ensure that the 
sum of the parts works as expected.

# Enter Front End Automation
In layman terms, front end automation testing is automating the workflow a
customer/user would go through using the product. For example, say we were
responsible for the automation for Facebook. What would the workflow look like?
Firstly, the test would have to login in as some mock user and check that the
login was successful. Next, it could try and post to the mock user's wall and
ensure that the wall posting functionality is working. 

The most used framework for front end automation testing is
[Selenium](https://www.seleniumhq.org/), and I'm going to be going over the
Selenium philosophy of front end testing in the next post.
