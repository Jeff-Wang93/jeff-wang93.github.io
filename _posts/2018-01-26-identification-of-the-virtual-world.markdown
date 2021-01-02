---
layout: default
title:  "Identification of the Virtual World"
date:   2018-01-26 16:27:04 -0800
categories: crypto security keys identification
---

# How can I send a message to a particular person?
If Alice wants to send a message to Bob over a network, how can she be
sure that Bob will be the only person who is able to read the message?

__*Public Key Encryption*__ is the most basic way of sending encrypted messages.
Under this encryption method, each person is assigned two keys: a 
__*public key*__ and a __*private key*__.

* The public key is available for everyone to see and is used to encrypt a 
  message that only a certain private key can decrypt. For example, say Alice 
  wanted to send the message `"Show Bob"` to Bob. She would use Bob's 
  **public key to encrypt the message** into some cipher.

* The private key is used to decrypt the message. Since the message was
  encrypted using a certain public key, only the corresponding private key can
  decrypt it. Imagine private keys as basically a person's signature.

Public Key Encryption is only as secure as the private keys. Say someone was 
able to steal Bob's private key. Now that person can pretend to be Bob and read
any message encrypted using Bob's public key. 

In addition, Alice can be sure that her message, assuming Bob's private key
wasn't compromised, can only be decrypted by Bob. On the other hand, Bob has
absolutely no clue who sent the message. Say he got that message `"Show Bob"` that
Alice sent earlier. Bob has no way of finding out who sent the message. 

# How can I tell who sent a message?
The public and private keys are inverses of each other. That means that messages
encrypted with a user's public key can be decrypted with the corresponding
private key and vice versa. If Alice really wanted to prove to Bob that she sent
the message `"Show Bob"`, she would encrypt the message using her private key.
Bob would then decrypt the message using Alice's public key. If the message is
successfully decrypted, then Bob knows Alice sent the message. In addition,
Alice cannot deny sending the message, assuming the private key was not
compromised of course.

# Enter digital signatures
These days, messages will tell who sent the message as well, this being
done through a __*digital signature*__. Let's use email as an example. Firstly,
say there's a message `"Hello World"` that Alice needs send to Bob. 
1. The plain text message will be fed into a hash algorithm to create a hash 
   of the message.
2. This hash is then encrypted using Alice's private key.
3. The encrypted hash is appended to the end of the plain text message and the 
   entire message + hash is sent.

When Bob receives the message, he needs to be sure the message itself wasn't
tampered with and that Alice was the one who sent the message.
1. Bob, using the same hash algorithm, calculates the hash of the plain text 
   message.
2. Bob then decrypts the encrypted hash using Alice's public key.
3. If the result of step 1 and step 2 match, then the message was not
   compromised, and Alice really was the sender of the message.

Of course, this was just a quick write up of the process. There's a lot more
that goes on. If interested, I would recommend looking up `digital
certifications`.

I'll bring up the concept of private/public keys in later posts.
