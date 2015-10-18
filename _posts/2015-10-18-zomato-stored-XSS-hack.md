------
layout: post
title: Bug#12 Zomato has stored XSS
published: true
-----

Last week, we discovered some more bugs, apart from the [11 we found earlier](https://medium.com/@fallible/we-discovered-severe-bugs-in-11-startups-worth-3-billion-in-a-week-cf2a856edb94). This was one of them, looks small in nature but seeing this, I suspect there are other Zomato pages which would be XSS prone.

**Company**: Zomato     
**Valuation**: $1 billion+     
**Bug**: The address field in Zomato orders on desktop version of the website is not sanitized before storing to database. This is a minor bug but can have embarassing implications. We have intimated their top execs.

![bbhack.png]({{site.baseurl}}/zomato1.png)

BTW the image did not render as it was being served over http and the page loaded over https, a Chrome protection against MITM attacks.

![bbhack.png]({{site.baseurl}}/zomato2.png)