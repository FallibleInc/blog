---
layout: post
title: How Fallible helps your startup
published: true
---



Startups are facing a new problem of data leak and loss of money & business. To be fair, the workload at startups is quite high. But at the same time, we cannot expect them to compromise with privacy of their customers. There are startups that deal with stuff that would be embarassing for customers if their order history is made public. Also, these leaks increase spam emails and SMSes.


### Our hypotheses -

- Startups have security bugs
- Automated security solutions do not discover all bugs and have lot of false positives. They are decent for XSS, SQL injection check but not for logic flaws, payment check, etc.
- Good security researchers are expensive for startups to hire. Some charge between $300-$500/hour


### The evidences -

- We discovered multiple vulnerabilites in more than 10 Indian startups in a week, each worth $100m+. Apart from these, we found several smaller startups that had bugs. We found a bug in a payment gateway/wallet service provider which is used by almost all ecommerce companies.

- Automated vulnerability scanners would not have been useful for most of the bugs we found. For dealing with situations where the outcome would be data leaks, problems in logic flow, payments etc. you need a capable security researcher.

- Security researchers are notoriously difficult to hire. A mere certification for pen testing does not give you enough skills. Some of the better ones charge $500/hour and would easily rake up a bill of thousands of dollars for couple of days of work.


### The Solution -

We provide you an insurance against security bugs. You pay us a premium every month and we ensure that there are no bugs in your system. If an external security researcher finds a bug, we work with them and award them a bounty that would be decent even by international standards. Our solution gives you,

 - testing of systems including web & mobile clients, APIs, ops using existing and homegrown automation tools.
 - an on-premise intrusion alert system to let you know of any abnormal activity with your APIs
 - a customized bug bounty program where reputed researchers can submit bugs, we verify their reproducibility and then alert you. You can use the fallible platform to work with the researcher to get it fixed and then we pay the bounty. You do not have to pay anything except for our monthly subscription.
