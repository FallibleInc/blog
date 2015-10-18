---
layout: post
title: Bug#12 Zomato has stored XSS
published: true
---

Last week, we discovered even more bugs, apart from the [11 we found earlier](https://medium.com/@fallible/we-discovered-severe-bugs-in-11-startups-worth-3-billion-in-a-week-cf2a856edb94). This was a small one, but can be exploited to a greater extent to get for example passwords of unsuspecting Zomato users using a carefully crafted attack.

**Company**: Zomato     
**Valuation**: $1 billion+     
**Bug**: The address field in Zomato orders on desktop version of the website is not sanitized before storing to database. This is a minor bug but can have embarrassing implications. We have intimated their top execs.

![zomato1.png]({{site.baseurl}}/zomato1.png)

BTW the image in the screenshot below did not render as it was being served over http and the page loaded over https, a Chrome protection against MITM attacks. The URL for the page below is [https://zoma.to/t/559053](https://zoma.to/t/559053)

![zomato2.png]({{site.baseurl}}/zomato2.png)

We discovered that the Zomato order status pages are public, so we curled their order history for last 500,000 orders, extracted food items, did a fuzzy string matching to match same items with different names and made a frequency tag cloud of the top 500 most ordered items.

![zomato-foods.png]({{site.baseurl}}/zomato-foods.png)


