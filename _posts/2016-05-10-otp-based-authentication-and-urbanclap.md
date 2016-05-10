---
layout: post
title: OTP based authentication 
published: true
---

*This is being published under responsible disclosure policy*

Almost every app today uses a 2 factor authentication where the second factor is an `SMS` sent to your mobile phone. This ensures that even if your password is compromised, you will be safe as long as you have your mobile phone with you.

##### Problem with OTP 
Problem comes when people use just `SMS` as the only form of authentication. Shortcuts in security are often disastrous. It would still have been okay if they implemented it perfectly. Far from it, OTP based authentications are subject to a lot of risks, sometimes:

* `send OTP` API sends back `OTP` in the API response (funny but true)
* They use very small OTP (convenient for users?)
* OTPs don't expire with time (ah, too much work already?)
* OTPs don't change with new generation request 
* unlimited generation of OTP is allowed (brute force)
* unlimited verification attempts are allowed (brute force)
* sometimes re-send OTP API sends back the `OTP` in the API response 

This can lead your account to be comprised and hence access all your details which you have saved in your account, access wallets in your account, place order on your behalf etc.

We have built a tool to capture such badly implemented OTP systems. 
![otp_tool.png]({{site.baseurl}}/otp_tool.png)

One such example was `UrbanClap`  which used to send the OTP back in the response of `re-send OTP` API :
![urbanclap_realtime.png]({{site.baseurl}}/urbanclap_realtime.png)

Timeline:

* 30/3 - Disclosed responsibly to Urbanclap
* 10/4 - They said they fixed it
* 11/4 - We checked iOS app, it had same issue with `send OTP` instead of `resend OTP`
* 11/4 - We again told them iOS still has the same issue 
* 1/5 - Still not fixed, sent a mail to check why aren't they fixing it
* 10/5 - Still no reply from them, disclosed publicly

This type of bug is more common than one might think. Its also weird to see people use different `APIs` for Android, iOS and web for the exact same purpose of OTP generation!

