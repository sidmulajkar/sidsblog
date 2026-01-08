---
title: "My personal thoughts on Mail Privacy"
categories: [personal thoughts on mail privacy, linux, email, privacy, security, sidsblog]
tags: [ personal thoughts on mail privacy, linux, mail, privacy, security, sidsblog]
date: 2023-12-26T17:26:04+05:30
description: "Personal thoughts on mail as how it is unsecure and privay concerns regarding the service."
author: Siddhant Mulajkar
draft: false
---


### Email still remains an Essential Backbone for communication, nearly used by ~(3-4) billion people. 

#### I do not use email as a privacy tool for communication. Check the last part**

---


The most private and secure way to communicate online is by using end-to-end encryption. If you send an end-to-end encrypted email, it’s encrypted on your device and isn’t decrypted until it reaches the device of the other person you sent the message to.

--


### Mail is Defacto not designed for privacy!

The data-safety concerns paved the way for many privacy-first email providers. Lavabit as an example, was the encrypted email service provider, was forced to comply or shutdown the businesss after the Snowden Leaks(now started again).

**Not every company stop their operations for normal people's rights, just like Lavabit.**

--

**LavaBit** >> https://youtube.com/watch?v=NM8fAnEqs1Q


![Lavabit Image](/images/emailser/lavabitemail.png)

--


> #### Email is more than communication – It’s your identity and worth protecting - Source ProtonMail

> Let's just move on to some generalized patterns...

--

#### Mail Stats > personal:   
+ 60-85% mails in my mailbox are from addresses based on Gmail-Gsuite and Outlook
+ 2-3% mails are from skiff proton that to my personal backups or some other product marketing mails.
+ Rest 10-12% are from other people using other mail service for campaigns, ads, newsletters, rss, podcasts etc.

--

For better default **privacy**, and not for sensitive use cases, you can still shift from **gmail** to other providers like **skiff or proton**. 

---

#### Q) >> Problem with the in-transit TLS Encryption?

When you send an email, your message is routed from server to server until it reaches your recipient’s inbox. All major email providers use TLS (Transport Layer Security), which provides an encrypted route for your email as it is sent between servers. This keeps your message private while it is in transit.

However, with TLS encryption, your emails are decrypted once they reach your email provider’s server rather than upon reaching your recipient’s device. This gives email providers that only use TLS access to all the messages stored on their servers.  -- {source ProtonMail Blogs - Lisa Whelan}


--


#### Then what about Proton Mail, Skiff, Tutanota, StartMail and other similar end-to-end encrpyted Mail Services?

--

#### Mails sent and received from skiff to skiff, proton to proton, or tutanota to tutanota are encrypted by default with the encryption keys.

--

##### If you send mails from either proton to skiff, skiff to tutanota, or viceversa...

###### The emails are not encrypted by default and are only encrypted in transit, and the mails that are received by the encrypted mail providers from other un-encrypted/encrypted providers are in plain format once recieved and then encrypted on their servers for storage. 

**Above statement is not true when using PGP** -- but the **subject line** is still **not encrypted** and metdata is collected even if you use the end-to-end encrypted providers, **unless you opt-out**, and some providers **don't** even let you opt out.

![Lavabit Image](/images/emailser/tuta-screen.png)

Statement reference links from the Encrypted Mail Providers >
[ProtonMail](https://proton.me/blog/zero-access-encryption)
[Tutuanota](https://tuta.com/blog/posts/what-is-end-to-end-encryption-why-it-matters)
[Skiff](https://skiff.com/blog/end-to-end-encryption-email)

--

"**As a Analyst, I would prefer looking at the metadata rather than the content** -- Edward Snowden"

--

#### What is end-to-end encryption Email?

If you send an end-to-end encrypted email, it’s encrypted on your device and isn’t decrypted until it reaches the device of the other person you sent the message to.

**However, end-to-end email encryption only works if both people are using PGP or the same E2EE email service, such as Proton Mail, Skiff or Tutanota.**








---

#### Conclusion

###### I do not recommend and use email as a privacy tool for communication, but still if you want to send me private data through mail, encrypt it using a file/folder and send it to me. - (Keep the Subject line simple)

I don't want to additionally rely on email providers for extra defence protection. If given a case, they might have to comply to the law to operate or shutdown the service.

How to encrypt and sign the file using the public PGP Key
- [using Windows Kleopatra](https://kevinsguides.com/guides/security/software/pgp-encryption)

- [using linux terminal gpg utility](https://itsfoss.com/gpg-encrypt-files-basic/) | [Another blog ref link](https://www.digitalocean.com/community/tutorials/how-to-use-gpg-to-encrypt-and-sign-messages)

use it as a **escalation** point to other better privacy alternative communication methods.

---

### Read More Blogs related to:

***[db-concepts]({{< relref "/tags/database/">}}) / [linux]({{< relref "/tags/linux">}}) / [flutter-installation]({{< relref "/tags/flutter">}}) / [networking]({{< relref "/tags/networking">}}) / [raspberry-pi]({{< relref "/tags/raspberry">}})***

--