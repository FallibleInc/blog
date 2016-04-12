---
published: false
---



We [wrote a post](https://fallible.co/blog/2016/03/30/payment-gateway-hacked-credit-card-leaked/) about security issues with some of the payment gateways in India. We wanted to tell more about the bugs at that point of time but we refrained from doing so as the vulnerabilites (the first in the list) were not fixed by the respective companies in their production systems. One of the companies which we reported the bugs to has confirmed the fix and we can do that now.


This issue was a complete credit card number leak along with the expiry date. We have blurred some of the digits of the full card (a sample response below). This system is comparatively small and was [used to process around 700,000 transactions per day](http://yourstory.com/2016/02/juspay-funding/), comparetely. The id can be enumerated to get card dumps for various users. The card blurred below is not our card and is most probably a debit card.

![Juspay1.png]({{site.baseurl}}/_posts/Juspay1.png)

Our previous post contained a list of companies, all of them using one or more of these systems. The list was obtained from the customer profile list of the respective vulnerable gateways. Even after explicitly specifying that these companies were not vulnerable by themselves and are using a vulnerable payment system, they were more interested in intimadation. We assume bullies just lack comprehension skills and have poor reading skills.


We were inundated by calls from ecommerce companies, payment gateways, PCI-DSS certifying agencies, card providers and journalists but we did not dislose the bug or the companies to any of them, even when some of them threatened to sue us (for nothing obviously). One surprising set of calls we got was from ethical hackers who kept on defending the companies that were leaking user data (wonder what was ethical about their defense). A PCI-DSS certification agency even went on to say that it was OK to leak any customer personal data as long as it did not invlove complete credit card numbers.



There were three set of negative responses.

1. This is a PR stunt - We find issues, inform companies so that they can fix them, inform users so that they can be alert and all you see is a PR stunt. Sure.

2. Why publish? - People wanted us to not publish anything and nobody will know when two year down the line some random user's card has a false charge. Also, protect the interest of companies who are not even our customers.

3. Why publish now? - We were very vague in details of the bug and we believe if a bug exposes customer data, then the customer has every right to know about it ASAP. Since we know that none of the previous 15 or so companies that we reported data leaks to did it and this was a severe case involving loss of money, we were compelled to do this ourselves.


We [believe that India needs a data breach intimation law like the US](https://www.whitehouse.gov/sites/default/files/omb/legislative/letters/updated-data-breach-notification.pdf) and strict 'enforceable' regulations to protect consumer interest as we move towards all things software. If you believe the same, please contact the relevant authorities in the goverment.








