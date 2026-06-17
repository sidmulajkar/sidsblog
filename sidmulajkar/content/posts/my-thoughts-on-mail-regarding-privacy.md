---
title: "My personal thoughts on Mail Privacy"
categories: [personal thoughts on mail privacy, linux, email, privacy, security, sidsblog]
tags: [ personal thoughts on mail privacy, linux, mail, privacy, security, sidsblog]
date: 2023-12-26T17:26:04+05:30
description: "Personal thoughts on mail as how it is unsecure and privay concerns regarding the service."
author: Siddhant Mulajkar
draft: false
---


---

### Email is still an essential backbone of communication

Nearly **~3–4** billion people use email today.

I still rely on it daily.

But I do not use email as a privacy tool for communication.


**This post explains why.**

---

### End-to-end encryption is the baseline for private communication

The most private way to communicate online is end-to-end encryption (E2EE).

### In a proper E2EE system:

- Messages are encrypted on your device
- They stay encrypted in transit
- Only the recipient’s device can decrypt them

This removes the service provider from the trust boundary for content access.

---

### Email was not built with privacy as the default

Email predates modern cryptographic communication models.

Most email today still works as:

```
Sender → SMTP servers → provider storage → recipient
```


Even with TLS:

- Data is encrypted in transit (server-to-server)
- But decrypted at provider level for processing and storage

This means:

```
> The email provider typically has access to message content at rest.
```

---

### Why privacy-first email providers exist

Concerns around data access and surveillance led to privacy-focused email services.

Examples include:

- Proton Mail
- Tutanota
- Skiff (historically)

A well-known historical case is Lavabit.

Lavabit was an encrypted email provider that shut down under legal pressure after the Snowden leaks and later restarted.

[https://youtube.com/watch?v=NM8fAnEqs1Q](https://youtube.com/watch?v=NM8fAnEqs1Q)

![Lavabit Image](/images/emailser/lavabitemail.png)

Not every provider exits under pressure.

But the incentive structure exists.

---

### Email is more than communication — it is identity

```
> “Email is more than communication – It’s your identity and worth protecting.” — Proton Mail
```

---

## Real-world email usage patterns (personal observation)

From my own mailbox:

- **~60–85%**: Gmail / Google Workspace / Outlook
- **~2–3%**: privacy-focused providers (Proton, etc.), mostly backups or product-related
- **~10–12%**: newsletters, campaigns, RSS, ads, marketing traffic

Email is still mostly infrastructure, not private communication.

---

### TLS does not equal end-to-end encryption

A common misunderstanding is equating TLS with end-to-end encryption.

TLS protects data:

- between servers
- during transit

But:

- Email is decrypted at provider servers
- Stored content is accessible to the provider in most standard setups

As described in Proton’s documentation:

```
> TLS encrypts data in transit, but does not provide end-to-end protection.
```


Source:
https://proton.me/blog/zero-access-encryption

---

### What about Proton Mail, Tutanota, Skiff, etc.?

Privacy-focused email providers use different models.

#### When both sender and receiver use the same encrypted system:

- Proton → Proton
- Tutanota → Tutanota

Messages are encrypted end-to-end using provider-managed keys.

---

### When sending across providers:

Example:

- Proton → Gmail
- Tutanota → Outlook

Then:

- Email is encrypted only in transit (TLS)
- Provider-side storage may be readable after delivery

---

### PGP changes the model

PGP enables true end-to-end encryption across providers.

However:

- Requires manual setup
- Not widely adopted
- Metadata (especially subject lines) is still exposed

Even with E2EE systems:

- Metadata leakage is still a major issue
- Subject lines are often not encrypted

---

### Metadata is still visible

Even when content is protected:

- sender/receiver
- timestamps
- subject lines (in many cases)
- routing information

As Edward Snowden has noted:

```
> “As an analyst, I would prefer looking at the metadata rather than the content.”

```

Metadata alone can be highly revealing.

---

### Example: encrypted email providers

Reference material:

- Proton Mail: https://proton.me/blog/zero-access-encryption  
- Tutanota: https://tuta.com/blog/posts/what-is-end-to-end-encryption-why-it-matters  
- Skiff: https://skiff.com/blog/end-to-end-encryption-email  

![Tutanota Screenshot](/images/emailser/tuta-screen.png)

---

### What end-to-end encrypted email actually means

A correct definition:

If you send an end-to-end encrypted email:

- It is encrypted on your device
- It remains encrypted until the recipient decrypts it locally

However:

- This only works when both parties use compatible encryption systems (PGP or same provider ecosystem)

Otherwise:

- Email falls back to standard server-mediated encryption (TLS)

---

### Conclusion

Email is still foundational infrastructure for communication.

But I do not treat it as a privacy-preserving communication channel.

If I need to share sensitive data:

- I encrypt files locally (PGP or equivalent)
- Then send encrypted artifacts over email
- Subject lines remain minimal and non-sensitive

Email providers may comply with legal requests depending on jurisdiction and operational constraints.

That risk model is not optional — it is structural.

---

## Encryption tooling references

- Windows (Kleopatra):  
  https://kevinsguides.com/guides/security/software/pgp-encryption

- Linux (GPG):
  https://itsfoss.com/gpg-encrypt-files-basic/  
  https://www.digitalocean.com/community/tutorials/how-to-use-gpg-to-encrypt-and-sign-messages

---

###  Closing note

Email is useful.

Email is universal.

But email is not inherently private.

If privacy matters, encryption must move to the file, not the inbox.

---

### Read More Blogs related to:

***[db-concepts]({{< relref "/tags/database/">}}) / [linux]({{< relref "/tags/linux">}}) / [flutter-installation]({{< relref "/tags/flutter">}}) / [networking]({{< relref "/tags/networking">}}) / [raspberry-pi]({{< relref "/tags/raspberry">}})***

--