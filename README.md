
# What is cdnguardian?
Right now? Not much.

Eventually, the idea is to have a script that can be run by crontab(every 24 hours?) to update your systems firewall with the list of IPv4 and IPv6 addresses that belong to CloudFlare, and allow only traffic to https. 

The effect would be your system only allowing TCP port 443 traffic from IPs that belonged to CloudFlare, which would reduce the attack surface of your system. This requires that Cloudflare is caching your **ENTIRE** site, however. As no assets would be retrievable by an end user if it wasn't in CloudFlare's cache, as their IP would not be among the whitelisted IPs.

# What systems are you targeting?

This initial release will target CentOS 7 64bit, with firewalld. Since systemd is becoming more and more widespread, this should work for the largest audience. 

# Where do you plan to take this(roadmap)?

In somewhat of an order of priority
* Error/sanity checking so the script does more good than harm, will need to be run as root or sudo
* Detect which firewall rules method is currently in use on the system, iptables/ip6tables or firewalld, and apply the whitelists accordingly.
* Save the rules for persistence across reboots based on the above detection.
* Easy way of reverting the changes this script makes
* Add support for additional CDN providers
 * Cloudfront?!
 * Fastly?!
 * MaxCDN?!
 * ?!


I want to eventually set the script to do a dig on my home router DDNS hostname  and add that as a whitelisted IP for SSH traffic. Same concept as above, but in addition to port 22 ssh traffic from my home router. Essentially locking my VPS from receiving traffic from anywhere but my home and the configured CDN provider.
