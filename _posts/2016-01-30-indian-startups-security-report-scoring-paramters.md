---
layout: post
title: Parameters used in scoring for public security dashboard
published: true
---




The following types of bugs were used while ranking startups and their systems for security issues. Almost all of the bugs relate to improper user input validation, lack of proper logic while implementation or not adhering to the principle of least privilege. 

	
### Authentication
1. Oauth redirection issue
2. OTP refresh/attempts/implementation issue
3. Destroy all active sessions on reset password/offer to 
4. Input validation registration data e.g.  javascript:// or data:// 
5. Uniqueness db constraints (account takeover/deletion by replacing email)
6. Expire session token after logout
7. Expire password reset links
8. Session/state fixation
9. OAuth open redirect in login
10. OAuth exposed auth token
11. OAuth fixation attack, missing state or unqiue token
12. Missing CSRF token auth
13. Improper UUIDs used as tokens (http://www.ietf.org/rfc/rfc4122.txt)
14. Invalidate OAuth token during revocation/denial HO 57603
15. Exposed Social login tokens in apps
16. Rate limiting/captcha after retries in reset password
17. Multiple registration using same unique identifier e.g. mobile

Let's look at this innocent looking User model that uses mobile number of users as it's primary key stored in form of string.

{% highlight python %}

class User(db.Model):
	mobile = db.Column(db.String, primary_key=True)
	email = db.Column(db.String(120), unique=True)

{% endhighlight %}

Now let's assume it has to send the mobile number as a big integer to a service for sending OTPs.
{% highlight swift %}

func sendMessage(mobileNumber: Int64, message: String) -> Bool {
    return true
}

func sendOTP(mobileNumber: Int64) -> Bool {
    let OTP = 1000 + arc4random_uniform(8999)
    let text = "Your OTP is \(OTP) and is valid for 15 minutes"
    return sendMessage(mobileNumber, message: text)
}

{% endhighlight %}

What is wrong here? Maybe the code below will clear things up. This is what happens in Python when you try converting a string to integer.

{% highlight python %}

>>> phone_no = "8121798285"
>>> phone_no_evil = "8121798285\n\n"
>>> int(phone_no) == int(phone_no_evil)
True
>>> phone_no == phone_no_evil
False

{% endhighlight %}


And, this is what happens when you try it in Swift

![Screen Shot 2016-01-31 at 2.30.24 AM.png]({{site.baseurl}}/swift.png)


### Configuration

18. Secure HTTP Headers (X-XSS, XFRAME, HSTS, CSP)
19. Secure, httponly cookies
20. SPF headers for main and marketing email domains
21. Dangling subdomain based takeover
22. SSL configuration based issues
23. Sensitive cookies without secure flag set
24. Directory traversal
25. AWS S3 buckets exposed
26. Credit card details or sensitive information over HTTP
27. Exposed backup files over public network
28. File disclousure

### Payments

29. Secret token leak in apps/API
30. Poor SDK implementation
31. Poor database design

{% highlight python %}

class Order(db.Model):
	id = db.Column(db.Integer, primary_key=True)

class Transaction(db.Model):
	id = db.Column(db.Integer, primary_key=True)
	order_id = db.Column(db.Integer, db.ForeignKey('order.id'), unique=True)
	payment_id = db.Column(db.Integer, db.ForeignKey('paymentgateway.id'))

class PaymentGateway(db.Model):
	id = db.Column(db.Integer, primary_key=True)

{% endhighlight %}

31. Weak salt /secret strength of provider
32. Server side data integrity verification for payment requests
33. Race condition in coupon redemption
34. Weak emunerable coupons
35. Poorly designed referral system

### Authoriation & Personal data 
36. Account details leak, missing authorization token
37. Project more data than required in API responses
38. Order History/information leak other than personal details
39. Working Authorization token (not only mere presence)

### Other attacks
40. CSRF/secure token expose over HTTP (possible MITM attack)
41. CRLF Injection attack
42. SQL Injection
43. XSS
44. SQL injection using cookies
45. CSRF token checks
46. Open Redirects
47. CSV Excel macro injection
48. Server side request forgery  https://goo.gl/aaxYr8
49. XXE /JSON based injection
