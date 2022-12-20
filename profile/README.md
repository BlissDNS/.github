# BlissDNS <br>
## Ad-Free, Encrypted, and Private DNS service. <br>
### What do we do? <br>
We are a public DNS service, free to use, that blocks ads, trackers, malware, and other nasy stuff that slows down or clutters your internet browsing experience. <br>
### How do I use BlissDNS? <br>
Easy, we have support for encrypted DNS with DNS-over-HTTPS, DNS-over-TLS, and DNS-over-QUIC. We of course support sending traffic directly to our IP so you can set your router or any device to use us for DNS if it does not support using encryption directly. <br>
We also support Android's Private DNS feature with the same URL below! <br>
### Our domain
DoH/DoT/DoQ domain: us1.blissdns.net <br>
### AdGuard Home/Similar
If you use AdGuard Home and want to use us as your upstream DNS servers, you can do so with the following as your upstream DNS! <br>
tls://us1.blissdns.net <br>
https://us1.blissdns.net/dns-query <br>
quic://us1.blissdns.net <br>
### Plain DNS/Pi-hole
If you are not using a service or device that takes advantage of encrypted DNS (Like Pi-hole or your router/game console/tv), you can send DNS queries our way at the following IP: <br>
173.255.201.254 <br>
<br>
# The details!
What exactly we do, what do we use, how is your information stored/kept/removed and why we do what we do.
### What do you do exactly.
We run AdGuard Home on a Linode server that utilizes Unbound for DNS resolution, we use Let's Encrypt and Certbot to keep our domain up to date with a valid SSL. <br>
### What blocklists do you use?
Well, our goal is to stay problem free 100% of the time while maximizing our effectivness. The lists we use are as follows: <br>
https://abp.oisd.nl/ <br>
https://github.com/badmojr/1Hosts/raw/master/Lite/adblock.txt <br>
https://raw.githubusercontent.com/CipherOps/AdList/main/Blocklist <br>
### How is my information safe?
We do collect non-anonymized logs for 24 hours, after which they're gone. Do know we only see what domain an IP looks up, we can see you go to google.com or reddit.com but nothing further than that, that information isn't transmitted via DNS so we are blissfully unaware of what you're doing, just what sites you visit. We do this because even in private beta we have to deal with spam bots, and with AdGuard Home we can see obvious signs of spam, see the IP doing it, and block it from the service, we maintain a public list of blocked IP's on our project in badips.txt. 
### Why are you doing this?
We hate ads, and trackers, and all the nasty crap you deal with online. We see people struggle to setup local adblocking or want adblocking on the go, and we do too, so instead of running personal VPN's and guiding others to set them up, we decided why not create a public server setup how we want, and let other people use it too, and thus BlissDNS was born.
