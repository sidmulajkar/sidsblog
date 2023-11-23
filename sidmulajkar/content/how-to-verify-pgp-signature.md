---
title: "How to verify PGP Key and PGP Signature"
date: 2023-02-02T19:09:26+05:30
draft: false
---

### Import signer’s PGP public key using URL…

Heads-up: replace https://sidmulajkar.com/gpg/sidmulajkar.asc with signer’s public key URL.

```
curl https://sidmulajkar.com/gpg/sidmulajkar.asc | gpg --import
```

or simply download the **PGP Public Key** using the **"Save As Feature"** of the browser...then,

```
gpg --import ./Downloads/sidmulajkar.asc 
```

```
sid@sid:~$ gpg --import ./Downloads/sidmulajkar.asc
gpg: key 24B58DCCC204D8AE: "Siddhant Mulajkar (sidmulajkar.com website) <hi@sidmulajkar.com>" not changed
gpg: Total number processed: 1
gpg:              unchanged: 1
```

imported 👍

---

List the key and verify the fingerprint manually given on the website or the source...

```
sid@sid:~$ gpg --list-keys
/home/sid/.gnupg/pubring.kbx
----------------------------
pub   rsa4096 2023-02-06 [SC]
      A74FCBC03330811F76E7A45424B58DCCC204D8AE
uid           [ unknown] Siddhant Mulajkar (sidmulajkar.com website) <hi@sidmulajkar.com>
sub   rsa4096 2023-02-06 [E]
```

for example, 

> PGP Fingerprint: A74FCBC03330811F76E7A45424B58DCCC204D8AE

--

---

### Verify signer’s PGP public key using fingerprint

Heads-up: replace hi@sidmulajkar.com with signer’s email and use published fingerprints to verify signer’s cryptographic identity 

```
sid@sid:~$ gpg --fingerprint hi@sidmulajkar.com
pub   rsa4096 2023-02-06 [SC]
      A74F CBC0 3330 811F 76E7  A454 24B5 8DCC C204 D8AE
uid           [ unknown] Siddhant Mulajkar (sidmulajkar.com website) <hi@sidmulajkar.com>
sub   rsa4096 2023-02-06 [E]

sid@sid:~$
```

---

### Verify signed message/file

```
gpg --verify ./Downloads/moneroadd.asc
```

```
sid@sid:~$ gpg --verify ./Downloads/moneroadd.asc
gpg: Signature made Mon 06 Feb 2023 11:42:19 AM EST
gpg:                using RSA key A74FCBC03330811F76E7A45424B58DCCC204D8AE
gpg: Good signature from "Siddhant Mulajkar (sidmulajkar.com website) <hi@sidmulajkar.com>" [unknown]
gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
Primary key fingerprint: A74F CBC0 3330 811F 76E7  A454 24B5 8DCC C204 D8AE
```

Good signature...👍

<!-- --

Also, you can verify the __Bitcoin__ and the __Monero__ address by opening the file in the new tab respectively, with ***Ctrl+C*** & ***Ctrl+F*** function

**This Signature file is signed for this website use...**

![Wallet Address Verification](/images/donate/bitcoinaddref.png)

--
 -->


Or to ***convert to original form of the file*** use the command

```
sid@sid:~$ gpg --output ./Downloads/moneroadd.txt --decrypt ./Downloads/moneroadd.asc
gpg: Signature made Mon 06 Feb 2023 11:42:19 AM EST
gpg:                using RSA key A74FCBC03330811F76E7A45424B58DCCC204D8AE
gpg: Good signature from "Siddhant Mulajkar (sidmulajkar.com website) <hi@sidmulajkar.com>" [unknown]
gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
Primary key fingerprint: A74F CBC0 3330 811F 76E7  A454 24B5 8DCC C204 D8AE
```

```
sid@sid:~$ cat ./Downloads/moneroadd.txt
monero:844cVdhQyvz4YqLrCk5XbQjH7UEm2QEmd5c7paxyU2XacVsSsPQ4CBWJ7iGFHjrAnRdJu3HRy9HtTeYC4kYHs1BvMysKVhQ
sid@sid:~$ 
```

---