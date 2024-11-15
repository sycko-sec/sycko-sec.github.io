---
layout: post
category: writeups
title: HTB Discounted Box
---


The Hack The Box challenge **"Discounted"** turned out to be a really fun and tricky Burp Suite exercise. I started by booting up the machine and running a quick Nmap scan to see what services were open. The scan showed an HTTP server, so I decided to check out the webpage.

![Untitled](assets/images/Discounted1.png)

When I opened the webpage, I found an online skincare store. Right on the homepage, there was a challenge: **"Task: Purchase Face Powder for $0 to obtain the flag."** There was also a discount code for 20% off any order. Right away, I had an idea of what might need to be done.

![Untitled](assets/images/Discounted2.png)

I launched Burp Suite to intercept traffic and figure out what was going on in the backend when the discount was applied to the Face Powder. After adding five Face Powders to my cart and applying the discount code, I noticed that the discount totaled $20. However, the discount amount would recalculate every time I removed an item from the cart, with the value set to `1` per item.

![Untitled](assets/images/Discounted3.png)


By tweaking the intercepted traffic, I found that changing the discount value from `1` to `0` stopped the recalculations when I removed items from the cart. After removing four of the Face Powders, the remaining $20 was covered by the $20 discount.

![Untitled](assets/images/Discounted4.png)

![Untitled](assets/images/Discounted5.png)

Finally, I sent the modified parameters using Burp Suite’s repeater tool, which successfully exploited the logic and gave me the flag! This challenge was a great reminder of just how powerful Burp Suite can be for solving these kinds of problems.