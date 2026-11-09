# BlissDNS

Free public DNS that blocks ads, trackers, malware, and other junk, for anyone who wants that on every device without running their own blocker.

Use it encrypted over DNS-over-HTTPS, DNS-over-TLS, or DNS-over-QUIC, or point your router or any device straight at our IPs.

## Quick setup

| Use it with | Address |
| --- | --- |
| DNS-over-HTTPS | `https://us1.blissdns.net/dns-query` |
| DNS-over-TLS | `tls://us1.blissdns.net` |
| DNS-over-QUIC | `quic://us1.blissdns.net` |
| Android Private DNS | `us1.blissdns.net` |
| Plain DNS, IPv4 | `173.255.201.254` |
| Plain DNS, IPv6 | `2600:3c00::f03c:93ff:feca:d2be` |

### Android

Settings, then Private DNS, then pick "Private DNS provider hostname" and enter:

```
us1.blissdns.net
```

The exact menu path depends on your phone, but it's usually under Network or Connections.

### Firefox, Chrome, or any Chromium browser

Turn on secure DNS (Firefox calls it DNS over HTTPS), choose a custom provider, and enter:

```
https://us1.blissdns.net/dns-query
```

### AdGuard Home or similar

Add these as your upstream DNS servers:

```
tls://us1.blissdns.net
https://us1.blissdns.net/dns-query
quic://us1.blissdns.net
```

### Routers, Pi-hole, game consoles, TVs

Anything that can't do encrypted DNS can use our IPs directly:

```
173.255.201.254
2600:3c00::f03c:93ff:feca:d2be
```

Plain DNS isn't encrypted, so your ISP can see your lookups. Use one of the encrypted options wherever your device supports it.

## How it works

Everything runs on a Linode server.

```
Plain DNS (port 53)   ->  dnsdist  ->  AdGuard Home  ->  Unbound
DoH / DoT / DoQ       ------------->   AdGuard Home  ->  Unbound
```

- **dnsdist** answers plain DNS on port 53 and filters out abuse before anything else sees it. It only handles plain DNS.
- **AdGuard Home** does the filtering, and serves DNS-over-HTTPS, DNS-over-TLS, and DNS-over-QUIC directly.
- **Unbound** does the actual DNS resolution.
- **[SDNS](https://github.com/semihalev/sdns)** is planned as a fallback resolver for AdGuard Home.
- **Let's Encrypt** and **Certbot** keep our TLS certificate valid.

### Abuse protection on plain DNS

Open DNS servers get used to attack other people. An attacker fakes their victim's IP, sends small queries, and DNS providers send big answers to the victim. So plain DNS on port 53 has a few rules:

- Queries from IPs on our [block list](https://github.com/BlissDNS/info/blob/main/badips.txt) are dropped with no response.
- `ANY` queries are dropped. Nothing legitimate needs them.
- `TXT` and `DNSKEY` queries over UDP get a truncated reply, and your device retries over TCP. That retry happens automatically. A faked IP can't complete a TCP connection, so the attack goes nowhere.

## Blocklists

Our goal is to block as much as possible without breaking anything. We use:

- [HaGeZi Fake](https://cdn.jsdelivr.net/gh/hagezi/dns-blocklists@latest/adblock/fake.txt)
- [HaGeZi Multi](https://cdn.jsdelivr.net/gh/hagezi/dns-blocklists@latest/adblock/multi.txt)
- [HaGeZi Native TikTok](https://cdn.jsdelivr.net/gh/hagezi/dns-blocklists@latest/adblock/native.tiktok.txt)
- [HaGeZi Threat Intelligence Feeds, IPs](https://cdn.jsdelivr.net/gh/hagezi/dns-blocklists@latest/adblock/tif-ips.txt)
- [HaGeZi Threat Intelligence Feeds](https://cdn.jsdelivr.net/gh/hagezi/dns-blocklists@latest/adblock/tif.txt)
- [OISD Big](https://raw.githubusercontent.com/sjhgvr/oisd/refs/heads/main/abp_big.txt)

We also host a mirror of these lists: https://data.blissdns.net/mirror/

## Privacy

We keep non-anonymized logs over a rolling 24 hour window to fight abuse. After 24 hours, they're gone.

By the nature of DNS, we can see which domains you look up. What you do on those sites is between you and them.

Requests from abusive IPs and requests for abusive domains are dropped with no response. Both lists are public:

- Blocked IPs: https://github.com/BlissDNS/info/blob/main/badips.txt
- Blocked domains: https://github.com/BlissDNS/info/blob/main/baddomains.txt

## Why we do this

We hate ads, trackers, and all the other crap you deal with online. We watched people struggle to set up local ad blocking, or want it on the go, and we wanted the same thing. So instead of running personal VPNs and walking others through setting them up, we built a public server set up the way we want and let everyone use it. That's BlissDNS.

## Contact

Questions, an ad domain we missed, or a domain we're blocking that we shouldn't be:

- Discord: https://discord.gg/Fk5VqxPD6U
- Reddit, comment in the megathread: https://www.reddit.com/r/BlissDNS/
- Issue tracker: https://github.com/BlissDNS/info/issues
- Email: info@blissdns.net

## Donate

We pay for everything out of pocket right now. Donations cover server costs and help us add servers in more countries.

**Patreon:** https://www.patreon.com/blissdns
