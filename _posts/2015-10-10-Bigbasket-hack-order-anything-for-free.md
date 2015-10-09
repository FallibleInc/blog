---
layout: post
title: "Bug#2 Order anything for free on BigBasket"
published: true
---

**Company**: BigBasket is an online grocery shopping startup based out of India.    
**Valuation**: $180 million+    
**Bug**: You just need to make a valid transaction once on Bigbasket (even cancel that order afterwards) and then use that transaction id infinite number of times. Note that the integer part of amount of the orders needs to be the same. This was due to a missing unqiue constraint on the transaction id which was being assigned to different order ids.


### Their response
BigBasket was responsive in their communication and their CTO along with VP Tech constantly keeping us updated and were quick to fix the bug. They even offered a token bounty of 5000 rupees in BigBasket credits, which we have not accepted.

![bbhack.png]({{site.baseurl}}/bbhack.png)
     
      
![bbhack2.png]({{site.baseurl}}/bbhack2.png)


### Bottomline
Please be extra careful while designing your database schemas and APIs, any obvious unique contraints should not be missed.


