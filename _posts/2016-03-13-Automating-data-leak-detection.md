---
layout: post
title: Automating data leak detection
published: true
---


We are creating a useful data leak detection tool. This article demonstrates what has been done till now.

Data leak is the most notorious bug a consumer facing software company encounters. Data leak may include disclosure of user’s phone number, email, home address, credit cards and other personally identifiable information.

Lot of the software companies fail to ensure that these informations are kept securely in their database. Sometimes they just leak database password. On the other times:

Basic authentication or authorisation are often absent in their API calls.
On top of that they use enumerable user ids, address ids or order ids.

A typical API will look something like this:
{% highlight javascript %}
http://www.mewantburger.com/v1/api/getUserAddress?userid=23781
{% endhighlight %}

And there would be no secure token in the headers (nor in the body) of the API calls, letting any user to do that API call from anywhere, the user doesn’t even have to be logged in to execute that API call successfully. One can simply run the following command from the terminal and get all the users addresses:

{% highlight bash %}
 $ for i in {1..25000}; do curl “http://www.mewantburger.com/v1/api/getUserAddress?userid=$i” ; done 
{% endhighlight %}
Some people will try to strengthen the security by making the userid longer like :

`10000023781`

Only that a human like you and me can easily see that first 6 digits are bogus and you only need to iterate from

`10000000000 to 10000025000`

Anyway, we saw these kinds of bugs too often in various companies, so we decided to try and make the detection of such bugs automated.

## The idea
We want to get all the APIs which leak data, so, we will record two different logged-in users activities (all the API calls) done while using the App / website. And then we will use the parameters like <email>, <userid> and <phone number> from user number 2 in the parameters of API calls done for user number 1. If the API call returns a valid response which matches the one for user 2, then it is leaking data, essentially.

For recording the activities one can use a proxy suite like burp or mitmproxy .

A typical users session will comprise of multiple requests and multiple responses:

{% highlight html %}
User 1                                   User 2

                
1. <Request A> <Response A>              1. <Request a> <Response a>

2. <Request B> <Response B>              2. <Request A> <Response A>

..........................               ..........................
..........................               ..........................

63. <Request C> <Response C>            63. <Request B> <Response B>

.......................                   ..........................
.......................                   ..........................

99. <Request Y> <Response Y>           105. <Request Y> <Response Y>

100. <Request Z> <Response Z>          106. <Request Z> <Response Z>
{% endhighlight %}


### Problem 1: 
##### We need to match the requests for both users. 
The serial order of Requests done for <user 1> is not a one to one match for the Requests for <user 2> since the recording of activities might have some noise in the API calls captured for example, Apple (in case of iOS) might be sending some stats to its server only adding to the noise for us to suffer — bad apple (of course not just Apple). So first, we need to match them 1 to 1.

We have done this matching by using the url and keys of query params and keys of params present in the body (json, form or multipart form) between the API calls listed for those 2 users. So, that works out to be *O(n^2)* . Yes, it can be improved and done in *O(n)* too, it is left as an exercise for the reader.

### Problem 2: 
##### We need to replay request of <user 1> with parameters from request of <user 2>. 
Now that we have one <Request, Response> from <user 1> and one <Request, Response> from <user 2>, we need to take some parameter values from <user 2> and replace it in the request of <user 1>.

What to take and what not to take?

For example if the developer did use the sessionToken to authenticate user but failed to validate the ownership of the userid then how will you confirm data leak? For example in this API:

{% highlight javascript %}
User 1:
http://www.mewantburger.com/v1/api/getUserAddress?userid=23781&sessionToken=gfbjasjkagaha3hj1syu6werwteio

User 2:
http://www.mewantburger.com/v1/api/getUserAddress?userid=50897&sessionToken=uursnwrckeoweyoehdbtuspwu46
{% endhighlight %}

Clearly if you replace the *session token* as well as *userid* then the request of <user 1> will essentially become request of <user 2> and that would obviously return the same response as it did for <user 2>. So we want to only replace stuff which an attacker can guess like *enumerable user id* or *email* or *phone number*

Now, we want to make this tool generic and should be able to detect such data leaks across multiple Apps and websites. So, checking for params matching letter to letter with ‘userid’ is not very useful. So, instead we will concentrate on the values of the parameters. An attacker can only enumerate smaller number maybe less than 8 or 9 digits in length. So we might user a regex like `\d{1–9}` and check all the values in the params of query or request body matching this regex. (And what if sessionToken also is a similar number. Then of course our method won’t work, but we assume that will rarely be the case.)

Similarly, other regexes can be used for `email`, `phone no.` or `order id`.

After replacing request 1 parameters, we need to replay it and see the response and that leads to our next problem.

### Problem 3: 
##### Verifying that the response is same as it was for <user 2>.
This is the phase we are in. Exact word to word match might not be ideal since the session token if any present in the response of this new request will be of <user 1>, what if response contains that token.

Other options could be :

* fuzzy match (but then what would be the threshold match percentage?)
* or regex match for information leak such as addresses, email, phone in the response body.


We will make the tool open source once it gets ready!
