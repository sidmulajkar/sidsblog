---
title: "Setting up Pi-hole as a recursive DNS server"
categories: [pihole, dns, sidblogs, setting pihole as recursive-dns, raspberrypi,raspberrypi-pihole]
tags: [pihole, raspberrypi, raspberrypi-pihole, dns, sidblogs, setting up pihole as recursive-dns, setting up pihole as recursive-dns using raspberrypi]
date: 2021-03-30T16:04:37+05:30
description: "setting up recursive dns using pihole for raspberrypi"
author: Siddhant Mulajkar
draft: false
---

**Got an old Raspberry Pi lying around? Hate seeing ads while browsing the web? Pi-hole is an open source software project that blocks ads for all devices on your home network by routing all advertising servers into nowhere. What's best is it takes just a few minutes to set up.**

![Pihole](/images/pihole-rdns/logo.png)

### What is a Pi-hole?
Network-wide ad blocking via your own Linux hardware. The Pi-hole® is a DNS sinkhole that protects your devices from unwanted content, without installing any client-side software.

##### What is a recursive DNS server?
The first distinction we have to be aware of is whether a DNS server is authoritative or not. If I'm the authoritative server for, e.g., pi-hole.net, then I know which IP is the correct answer for a query. Recursive name servers, in contrast, resolve any query they receive by consulting the servers authoritative for this query by traversing the domain. Example: We want to resolve pi-hole.net. On behalf of the client, the recursive DNS server will traverse the path of the domain across the Internet to deliver the answer to the question.

##### Web Interface

![Pihole-web](/images/pihole-rdns/dashboard.png)


# Pi-hole as All-Around DNS Solution
**The problem: Whom can you trust?**
Pi-hole includes a caching and forwarding DNS server, now known as FTLDNS. After applying the blocking lists, it forwards requests made by the clients to configured upstream DNS server(s). However, as has been mentioned by several users in the past, this leads to some privacy concerns as it ultimately raises the question: Whom can you trust? Recently, more and more small (and not so small) DNS upstream providers have appeared on the market, advertising free and private DNS service, but how can you know that they keep their promises? Right, you can't.

Furthermore, from the point of an attacker, the DNS servers of larger providers are very worthwhile targets, as they only need to poison one DNS server, but millions of users might be affected. Instead of your bank's actual IP address, you could be sent to a phishing site hosted on some island. This scenario has already happened and it isn't unlikely to happen again...

When you operate your own (tiny) recursive DNS server, then the likeliness of getting affected by such an attack is greatly reduced.


### Setting up Pi-hole as a recursive DNS server solution

We will use unbound, a secure open-source recursive DNS server primarily developed by NLnet Labs, VeriSign Inc., Nominet, and Kirei. The first thing you need to do is to install the recursive DNS resolver:

```
sudo apt install unbound
```

**Configure unbound**

Highlights:

- Listen only for queries from the local Pi-hole installation (on port 5335)
- Listen for both UDP and TCP requests
- Verify DNSSEC signatures, discarding BOGUS domains
- Apply a few security and privacy tricks using your presonal preferred text editor or use **nano** to copy the given code below in the path mentioned next line.
```
sudo nano /etc/unbound/unbound.conf.d/pi-hole.conf
```
```
server:
    # If no logfile is specified, syslog is used
    # logfile: "/var/log/unbound/unbound.log"
    verbosity: 0

    interface: 127.0.0.1
    port: 5335
    do-ip4: yes
    do-udp: yes
    do-tcp: yes

    # May be set to yes if you have IPv6 connectivity
    do-ip6: no

    # You want to leave this to no unless you have *native* IPv6. With 6to4 and
    # Terredo tunnels your web browser should favor IPv4 for the same reasons
    prefer-ip6: no

    # Use this only when you downloaded the list of primary root servers!
    # If you use the default dns-root-data package, unbound will find it automatically
    #root-hints: "/var/lib/unbound/root.hints"

    # Trust glue only if it is within the server's authority
    harden-glue: yes

    # Require DNSSEC data for trust-anchored zones, if such data is absent, the zone becomes BOGUS
    harden-dnssec-stripped: yes

    # Don't use Capitalization randomization as it known to cause DNSSEC issues sometimes
    # see https://discourse.pi-hole.net/t/unbound-stubby-or-dnscrypt-proxy/9378 for further details
    use-caps-for-id: no

    # Reduce EDNS reassembly buffer size.
    # Suggested by the unbound man page to reduce fragmentation reassembly problems
    edns-buffer-size: 1472

    # Perform prefetching of close to expired message cache entries
    # This only applies to domains that have been frequently queried
    prefetch: yes

    # One thread should be sufficient, can be increased on beefy machines. In reality for most users running on small networks or on a single machine, it should be unnecessary to seek performance enhancement by increasing num-threads above 1.
    num-threads: 1

    # Ensure kernel buffer is large enough to not lose messages in traffic spikes
    so-rcvbuf: 1m

    # Ensure privacy of local IP ranges
    private-address: 192.168.0.0/16
    private-address: 169.254.0.0/16
    private-address: 172.16.0.0/12
    private-address: 10.0.0.0/8
    private-address: fd00::/8
    private-address: fe80::/10
```

##### Configure Pi-hole

Finally, configure Pi-hole to use your recursive DNS server by specifying **127.0.0.1#5335** as the Custom DNS (IPv4):

![Pihole-web](/images/pihole-rdns/recursiveresolve.png)

**(don't forget to hit Return or click on Save)**

**Lastly, restart unbound:**

```
sudo service unbound restart
```

-------------------------------------------------------------------------------
**And that’s it! New unblocked DNS requests will be made directly to the authoritative servers instead of routing through a third party dns services like Quad9 or Google, etc.**
-------------------------------------------------------------------------------

