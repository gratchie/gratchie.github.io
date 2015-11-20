---
layout: post
title: "Setting up Squid / Proxy Server"
published: true
tags: squid proxy
---

None of our client VM's have direct access to internet so we'll setup a proxy server that the machines can use to acess internet and do external yum installs from time to time.

* Install squid proxy

    `yum -y install squid`

* Edit /etc/squid/squid.conf . Add your local network that will use the proxy server. The rest of the default options can stay. 

    `acl localnet src 192.168.88.0/24`

* Start squid

    `systemctl start squid`

* Enable on boot

    `systemctl enable squid`

* Add this line to your client's /etc/yum.conf to enable proxied yum install

      `proxy=http://proxy.gracie.net:3128`
