---
layout: post
title: "Bug#13: Zo Rooms leaks all users personal and bookings data"
published: false
---



**Company**: Zo Rooms, started in 2015, aggregates budgets hotels. They have raised more than 300 crores INR ($45m+).      
**Valuation**: $100m+ (approximated) 

Last week, we discovered even more bugs in potential Indian unicorns, taking our count to 19 from the [11 we discovered earlier](https://medium.com/@fallible/we-discovered-severe-bugs-in-11-startups-worth-3-billion-in-a-week-cf2a856edb94). 

We mailed about the vulnerabilites to Zo Rooms customer support and received no reply. After waiting for 4 days, we mailed to the 7 co-founders of Zo Rooms and their head of products but the mails went unreplied.
![zorooms.png]({{site.baseurl}}/zorooms.png)

         
We then added their CEO and co-founders in a Whatsapp group and informed them about the mail.We received a curt 'Thanks' but still no reply on the mail. We remembered this was the same CEO who devoted a [lot of time to write awesome 2000 words answers and advices on Quora with great illustrations](https://www.quora.com/Business-Ideas/What-are-the-best-ways-to-think-of-ideas-for-a-startup/answer/Dharamveer-Singh-Chouhan?share=1). We were disappointed with the response.

     
![zorooms-wa1.PNG]({{site.baseurl}}/zorooms-wa1.PNG)

![zorooms-wa2.PNG]({{site.baseurl}}/zorooms-wa2.PNG)

     
          

**Bugs**:      

1. Zo Rooms leaks users past and future booking data in one of their API responses. This URL does not rely on authorization token to validate booking id against current logged in user. Since, the booking id are simply sequential integers instead of something like a secure UUID, they can be curled over.  There is another URL which has the same issue and spits out customer data including phone number, email and addresses on file. The number of affected users stands at a little over 200,000.

2. Zo Rooms has an exposed API endpoint which takes in parameters like transaction id, amount, product info etc., concatenates it in a certain way according to a certain payment gateway provider specifications and generates two hashes to be used to verify that the user indeed paid the amount requested, one before the transaction and one after it. Using this URL to generate a different hash with a smaller amount for ingoing and the correct hash with correct amount for outgoing can allow a malacious user to book a Zo Rooms property for lesser amount.

The first bug is more dangerous and can be exploited in several different ways both online and in physical space.

- A sophisticated burglar may take advantage of the fact that a certain person would be away on a certain date, and can target their house.
- Usual spams and phishing attempts (and the Facebook and Google Ads targeting by competitors who may already have gained access to the data). Competitors may also benefit from the order size data (amount, orders, frequency, repeat customers, dropoff, discounted customers behavior, vendor details).
- If your hotel booking with Zo Rooms was supposed to be a discreet time away with someone, it is out in the open now.
       

The disturbing fact we found is that not a single co-founder among the more than a half-dozen seemed to care to respond to our email. We hope this blog post reaches them and the bug is fixed.


###Lessons:      
- Do not ever project more data from your APIs than you need to show to user in a view. 
- Use authorization checks against current logged in user and make all API endpoints private by default.
- Kindly reply to people who are finding your bugs and helping you get them fixed for free. It is a decent thing to do.
