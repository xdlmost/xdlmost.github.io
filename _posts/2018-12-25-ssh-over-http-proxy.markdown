---
layout: post
title:  "ssh over a http proxy"
date:   2018-12-25 15:00:00 +0800
categories: linux
---

# ssh over a http proxy

## 1- problem
At my work place,I need to connect to a server in pulic internet vis ssh.But we can't approach to any resource in pulic internet whitout a http proxy.So let find a way to use ssh over a http proxy.

## 2- solution

I find a way to use ssh over a http proxy

1. install **corkscrew**

corkscrew is a proxy that tunnel TCP connections through HTTP proxies.

``` bash
sudo apt-get install corkscrew
```
2. config ssh

the config file of ssh is located in `~/.ssh/config`. if there is no such file ,just create it. and add a `ProxyCommand`. that will work.

```bash 
vim ~/.ssh/config

# add a line in ~/.ssh/config
ProxyCommand /usr/bin/corkscrew {http_proxy_ip} {http_proxy_port} %h %p
```
so,all connect will go through http proxy.
if you want only several target go through http proxy,you can add `Host` key word to you ssh config file like this.

```
#  ~/.ssh/config

Host {target server}
    ProxyCommand /usr/bin/corkscrew {http_proxy_ip} {http_proxy_port} %h %p

```

## references
[https://daniel.haxx.se/docs/sshproxy.html](https://daniel.haxx.se/docs/sshproxy.html)

[mtu.net/~engstrom/ssh-through-http-proxy/](mtu.net/~engstrom/ssh-through-http-proxy/)
