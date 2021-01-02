---
layout: post
title:  "The Wonderful World of Hashing"
date:   2018-01-26
categories: hashing cryptography security
--- 

# What is a cryptographic hash?
For a basic definition, in terms of computer science, a __*hashing algorithm*__ is an 
algorithm that takes in some data and compresses it to a string of fixed length
(length dependings on which algorithm is used). This output string is called a
__*hash*__.

For example, if we took the sentence `I hate the fish in my fish tank` and fed 
it into a hash algorithm (here, we're going to be using the **MD5** algorithm), 
we would get `005952D2E7FDE0B719E104C4CEC62A60` as output. This long 
string of seemingly random characters is our hash.

So, now that the definition of a hash is out of the way, what is cryptographic
hash? A cryptographic hash is a hash function specifically used for
cybersecurity. The main features of a cryptographic hash algorithm is that it 
produces an **irreversible and unique result**. 

* **Irreversible**  means that if I gave you the above hash (`005952D`...), you 
would **not** be able to get back `I hate the fish in my fish tank`. Thus, the
original data is allowed to remain secure and unknown by anyone who just has 
the hash.

* **Unique** means that two different inputs will never result in the same output. 
So the above hash (`005952D`...) will only ever be given as output if 
`I hate the fish in my fish tank` is fed as input. For further explanation,
let's look at the table below:

| Input (MD5 Algorithm)  | Output |
| :---------------------- | :------ |
| `I hate the fish in my fish tank`  | `005952D2E7FDE0B719E104C4CEC62A60` |
| ---
| `I hate the fish in my fish tank!` | `AAD0BD1E2BBDE49619B2A3F14EAA20F7` |
| ---
| `I Hate The Fish In My Fish Tank`  | `21ABF7988A638B3FCA98E2FBE113A2D1` |  
| ---
| 
{: rules="groups"}    
   
As you can see, simple changes, such as adding a `!` to the end or 
capitalizing every word results in completely different hashes. This is
important because it increases the pool of available hashes, which deters brute
force attacks. In other words, We're basically trying to make it so that an 
attacker can't just have his/her machine try every possible combination. 

# What are the uses of a cryptographic hash?
A simple example could be user passwords. When you log into a website that
requires a login, chances are your passwords are being stored as hashes (if the
website actually cares about security) on the website's databases. When you 
enter your password, that password gets fed into whatever hashing algorithm the 
website uses and the resulting hash is compared to what was stored on the 
website. If the two hashes match, then the password is correct for that 
specific user. The reason websites store hashses is because, if a website's 
databases were ever compromised, the attacker would only obtain hashes and not 
the actual, readable passwords. This is another reason why **irreversibility**
is such an important feature of a cryptographic hash algorithm.

Unfortunately, some websites do not utilize cryptographic hash algorithms, and
just store passwords in **plain text**. This means that if an attacker was ever 
able to compromise these sites' databases, they would receive the actual, 
readable password. If you ever see some article about a website storing 
sensitive information in plain text, this is why it's bad. 
