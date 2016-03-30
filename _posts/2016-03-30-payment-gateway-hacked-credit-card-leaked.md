---
published: false
---

## Used your credit card online in India? it may already have been stolen

During the past several months, we have discovered full credit card details leak from one of the most popular PCI DSS Level 1 certified payment gateway. The gateway claims to do more than 15,000,000 transactions on a monthly basis.  Another popular payment gateway is leaking partial credit card and user personal information which can be used to engineer a variety of attacks. In addition to this, we have found a severe vulnerability in the way a third popular payment gateway implements its request data integrity protection which can be cracked using a single commodity gaming PC within a week, thus allowing free access to virtually anything that is being sold online in India and the transaction history of users.

We have already intimated the respective payment gateways and they are working on the fix, but we are afraid we might not have been the first to discover this vulnerability. Since Indian Law does not have a data breach intimation law like the US (https://www.whitehouse.gov/sites/default/files/omb/legislative/letters/updated-data-breach-notification.pdf) and based on our experience intimatating severe data leaks to more than 15 companies, we do not think the companies will ever make this information known to their end users.

This is a general notice to the public to ensure that their cards are safe. Hackers generally do not attempt to use all the cards as soon as they get access to it so it is requested that you monitor your charges and statements or better disable current cards if possible. Domestic only debit cards which cannot ever work without CVV/ PIN and OTP can be assumed to be safe. 

Some of the companies who use these vulnerable gateways include BookmyShow, Foodpanda, Freecharge, Mobikwik (this is not the gateway mentioned above), Uber, Ola, Snapdeal, Rupay, Makemytrip, Yatra, Swiggy, Redbus, Voonik (Please note these companies are not vulnerable, at least related to above bugs) -

We will come back with more information regarding these issues once the respective companies have fixed the bugs. We know that no company wants to leak their customer’s payment and personal data and it will be a difficult and time intensive task to fix some of these issues.

We at Fallible are building products to secure large organizations and startups alike. Contact us at hello@fallible.co
