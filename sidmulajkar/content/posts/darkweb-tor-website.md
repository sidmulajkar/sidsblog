---
title: "How to create a tor based website?"
categories: [tor, dark web, tor browser, cloud services, raspberry pi, microservices, onion website, sidsblog]
tags: [tor, dark web, tor browser, cloud services, raspberry pi, microservices, onion website, sidsblog]
date: 2022-05-30T17:26:04+05:30
description: "In this blog, we will learn how to create a tor based website and do we actually need it."
author: Siddhant Mulajkar
draft: false
---


### What is a tor website?
A top-level Internet domain used by anonymous websites on the Dark Web.

For eg, as we go to any other website such as google.com or youtube.com, DuckDuckGo is an internet search engine such as google that emphasizes protecting searchers' privacy,

can also be accessed using duckduckgo.com or also using the tor address of the website

https://3g2upl4pq6kufc4m.onion (using the tor browser)

---

### Why do we need even need it?

There are two main reasons why people may use the 'Dark Web':

1. Anonymisation

    People may have many reasons for protecting their online identity.

2. Accessing 'Hidden Services'

    A Hidden Service (also known as an 'onion service') is one **where not only the user but also the website itself, have their anonymity protected by Tor**. 
    
    **This means that the IP address of the site cannot be identified, meaning that information about its host, location, or content is hidden.** Hidden Services are sometimes called “onion addresses” because the website name often ends .onion.


The people who need the Dark Web so they can keep doing their dangerous – **but not necessarily illegal**– work are:
- Whistleblowers
- Dissidents of oppressive regimes
- Activists
- Journalists who must protect their sources
- Law enforcement
- Intelligence agencies

As you’d expect, misguided individuals or those with clear criminal intent have found a way to use this level of anonymity to cover up their illicit activities and – up to a point – evade law enforcement.

---

**Is it legal?**

**Using Tor or visiting the Dark Web is not unlawful in itself**. It is of course illegal to carry out illegal acts anonymously.

Want to learn more about how does the **tor** works?
https://cybernews.com/privacy/what-is-tor-and-how-does-it-work/


![How does tor work](/images/torwebsiteblogdata/toworking.png) 


Credit: NetworkChuck

---

### Okay, How to create a tor-based website?

We can create it using a **Raspberrypi, Virtual Machine, or simply host it on any cloud services such as Google Cloud, AWS, or Azure Webservices**. 

We can also use some other options like **Linode, Relpit(Free Version), or Heroku(Free)**.

In this blog, we are simply creating this tor website by creating the **Virtual Machine** of the ubuntu server.

---
**Steps:**

1. Create a Virtual Machine using any distro you like for the project or if you are using the Linux machine then no need to create the VM. 

(or if you are **having a raspberry pi** just install the raspbian os and follow the other steps as they are similar)

![VM using UbuntuServer](/images/torwebsiteblogdata/ubuntuserver.png) 


2. Simply, login to the VM and update it(might take around 10-15mins on the first boot update and then reboot it for all packages to work properly)

```
sudo apt update
```


![VM Update](/images/torwebsiteblogdata/update.png) 


3. Install the tor and the Nginx for the tor website to work using the commands (you can use apache as well if not Nginx, link to that article is mentioned below at the end)

```
sudo apt install tor
```

```
sudo apt install nginx
```
![Tor and Nginx Install](/images/torwebsiteblogdata/tor1.png) 



4. So we are going to modify some of the lines of tor configuration to make it work

```
sudo nano /etc/tor/torrc
```

is the file we are modifying, just search for **HiddenServiceDir and HiddenServicePort** as shown in the next image, uncomment them and save them using Ctrl+X, Ctrl+S.

![Tor Config](/images/torwebsiteblogdata/torcconfig.png) 

![Tor Config](/images/torwebsiteblogdata/torrc2.png) 

**The HiddenServiceDir** stores the public and the private key and our .onion address is stored

**The HiddenServicePort** exposes the localhost on the port 80 for other people to access it, just as any other website using the HTTP protocol.


5. Check whether both the services are running properly and perform a restart operation after the changes made to the tor service.

```
sudo service stop tor
sudo service start tor
sudo service tor status
```

![Tor Service Working](/images/torwebsiteblogdata/torservice.png) 


Similarly check for Nginx,

![Nginx Service Working](/images/torwebsiteblogdata/nginx.png) 


6. Now we can check our **.onion address** using the command

```
sudo cat /var/lib/tor/hidden_service/hostname
```

![Onion Address](/images/torwebsiteblogdata/toraddress.png) 


7. Now, we can finally check our website using the address just we got with the help of tor-browser

![Tor Website](/images/torwebsiteblogdata/onionwebsite.png) 


8. Need to modify some more lines of the Nginx to make it safer to access

```
sudo nano /etc/nginx/nginx.conf
```

we need to uncomment highlighted lines and also add one more line.

```
port_in_redirect off;
```

![Nginx Config](/images/torwebsiteblogdata/nginxconf.jpeg) 


and then restart the Nginx server for one more time

```
sudo service nginx restart
```

---

**Hola!!!** We have our tor website up and running and we can modify it to our heart's content and make it up and live to the world.

**We can simply access this website using the tor address without the need to dynamically set the IP to the domain name service or without extra hassle until the VM, raspberry pi, or Cloud Instance is running. It can be accessed fron the local network or either from the outside network as well.**

---

We can change the details or redesign the website by modifying/adding more pages in the directory

```
/var/www/html 
```

![Nginx Config](/images/torwebsiteblogdata/websiteredesign.png) 


---

Link to the Apache Blog if you want to use Apache instead of Nginx:

https://medium.com/axon-technologies/hosting-anonymous-website-on-tor-network-3a82394d7a01

---

### Conclusion:

Tor offers anonymous browsing capabilities to people across the world. Users located in countries with strict censorship laws can use it to access restricted sites like Facebook, Google, foreign news websites or forums privately.

To keep it simple, using Tor makes it more difficult (but not impossible) for Internet activity to be traced back to the user.

Despite these noble goals Tor also has a dark side. Obviously, the convenient (and relative) anonymity attract people with some less honorable intentions.

---