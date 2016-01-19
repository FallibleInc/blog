---
layout: post
title: "Bug#1 Delete all BookMyShow accounts and wallets"
published: false
---


*[This bug is a part of the vulnerabilites we discovered in 11 Indian startups worth $3 billion+ in a week.](https://medium.com/@fallible/we-discovered-severe-bugs-in-11-startups-worth-3-billion-in-a-week-cf2a856edb94)*

    
**Company**: BookMyShow is an Indian ticketing platform for movies, events etc.    
**Valuation**: 1000 crores+ ($170 million+)    
**Bug**: You can overwrite anyones profile on BMS with your own effectively deleting their account and their newly introduced BMS wallet. If the unsuspecting user does not check their profile before putting some money into their wallet, the money goes to the hacker's wallet. Also, once an account is overwritten, there is no way to login or activate the account, even by password reset on the user side thus rendering it useless.

### Their response
After multiple mails, and a video that we created using mitmproxy to show them that there indeed was a bug, they just said that they will look into it. There has been no response to our mails confirming that the bug has been fixed. But we did verify it yesterday and they have fixed the bug and silently ignoring our emails. A token thank you mail would have been a nice gesture.

![bookmyshow hack.png]({{site.baseurl}}/bookmyshow.png)


### Bug video proof

We had to create a demo video using mitmproxy for BMS developers to demonstrate that there actually was a bug, since their CEO was not paying attenion. The victim account is named 'Md. Haaris' and it would be overwritten by account named 'Manish'.

<iframe width="420" height="315" src="https://www.youtube.com/embed/3jWQImzQzQ0" frameborder="0" allowfullscreen></iframe>

### Bottomline

Startups need to be more careful with authorizaton checks and token. When designing an API, every data except the public ones should need the authorization token and be matched against the current user.
