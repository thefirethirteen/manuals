---
title: Wireguard
---

+ This guide is WIP<br/>
+ This guide also offers an introduction to VPNs in general, to make you plan what to use Wireguard for :) <br/>
+ This guide also assumes you are using GNU/Linux<br/>

# Introduction

[Wireguard](https://wireguard.com) is a fast, simple and secure VPN solution available on all major operating systems. <br/>

### Why would you want a VPN

Say you want to open a Minecraft server but you don't want to make it accesible via the open internet due to [some dubious crawlers :)](https://invidious.flokinet.to/watch?v=fvbVnT-RW-U). <br/>
With a VPN, friends can securely join your server using an encrypted tunnel, so nobody on the open internet can see what you're doing. <br/>

Another obvious usecase is to browse the internet with a different IP. VPNs can also act as glorified proxies tunneling your internet traffic from your <br/>
main PC to the VPN server. This is helpful for accessing region-locked sites, bypass ISP blocked websites, and more. <br/>

> For the more tech-saavy people reading this, I bet you know about VPN as a service such as NordVPN. Bear in mind the IPs <br/>
big VPN providers use are usually blacklisted by some websites, so hosting a VPN solution yourself can help with this. <br/>

### Wireguard in comparison with other VPN solutions

I believe you're accustomed with OpenVPN, the most popular VPN stack. Although it's a very good option even to this day, <br/>
is robust and audited countless times, it started to show its age. Its encryption is made with a bloated TLS stack, significantly <br/>
hurting its network performance. If you are working in networking, perhaps you've also heard of IPSec. Although significantly better <br/>
network performance, it's painfully difficult to set up and in general is a no-go for beginners. <br/>

Wireguard is fast, really really [fast](https://www.wireguard.com/performance/), due to its lighter crypto stack, smaller code base <br/>
and it's running in [kernel space](https://github.com/torvalds/linux/tree/bfa3037d828050896ae52f6467b6ca2489ae6fb1/drivers/net/wireguard) while the other implementations run in userland <br/>
(significantly hurting the performance due to the userland scheduler being more agressive and other technical challenges).<br/>
But Wireguard is also capable of running in userland if the OS does not have the possibility to execute in kernel space (looking at you Google)<br/>
with implementations made in [Go](https://github.com/WireGuard/wireguard-go) and [Rust](https://github.com/cloudflare/boringtun) <br/>

# Installation

Wireguard's kernel module should be included in all major Linux distributions. To check run <br/>

```
lsmod | grep wireguard
```

If it displays some line containing the keyword, you're good to go, otherwise you have to activate by running<br/>

```
modprobe wireguard
```

As superuser.

> WARNING!!! Although people have attempted to make Wireguard work in Linux container enviroments like docker,<br/>
it's a massive undertaking for beginners since you have to fight with the container network stack, which, to be<br/>
totally honest, needs a lot of work ~(netavark you had one job and failed miserably listening to DNS queries in the default namespace)~.

Don't forget to also install the Wireguard userland tools.

```
apt install wireguard-tools
pacman -S wireguard-tools
apk add wireguard-tools
emerge -a wireguard-tools
dnf install wireguard-tools

you get the idea
```

## Packet forwarding

By default, if you want to communicate with another device within the same VPN network, <br/>
you cannot ping or connect to it because the server is dropping the packets(not sending to the destination).<br/>
Below is an illustration of what happens if nothing is done:

```
    +--------------------------+         +-----------------------------+
    | Client device - 10.1.7.3 | ------> | Wireguard Server - 10.1.7.1 |
    +--------------------------+         +-----------------------------+
                                                  |
    ping 10.1.7.2                                 |
    100% packet loss                              |
                                        
                                                    <- net.ipv4.ip_forward=0
                                        
                                                  |
                                                  |
                                                  ^
                                          +-------------------------+
                                          | Target device - 10.1.7.2|
                                          +-------------------------+

```
In order to mitigate this, we have to allow IP forwarding, basically, tell the server that it should redirect the packet<br/>
to the destination.

So inside `/etc/sysctl.d/99-sysctl.conf` write

```
net.ipv4.ip_forward=1
```

and then instantly apply the change by executing `sysctl -w net.ipv4.ip_forward=1`.

## Generating Wireguard keys

Wireguard uses an assymetric key-pair authentication to establish the tunnel. Each device must have a public key and private key.<br/>

```
    +--------------------------+         +-----------------------------+
    | Client device - 10.1.7.3 | <-----> | Wireguard Server - 10.1.7.1 |
    +--------------------------+         +-----------------------------+
     Interface: WG-Client                 Interface: WG-Server
     Endpoint: server.wireguard:1234      Listen-Port: 1234
     Private key: uBPmgZwnAK.........     Private key: ONpma...........

     Peer: cJCMdhGL..................    Peer: hHJjdfJf................
```

Lost? Yeah, let me try to explain. The client device must first connect to the Wireguard server over the internet, which is why <br/>
the `Endpoint` and `Listen-Port` are specified. But both devices need to authenticate in order to establish the encrypted link. <br/>
Each device generates a private key, and with that they also make a public key which looks nowhere near similiar to the private key. <br/>
Now, they share each other's public key under `Peer` to know which trusted device is part of the network. You can have multiple peers. <br/>

```
    +-----------+                                                   +-----------+
    | WG-Client | --------------->------------------<-------------- | WG-Server |
    +-----------+               /                    \              +-----------+
         |                     /                      \                     |
    Private key -> Public key /                        \  Public Key <- Private key
```

The easiest way to generate a key pair is with this command on each machine:

```
wg genkey | tee privatekey | wg-pubkey > publickey
```

Let's go one by one. `wg genkey` randomly generates a private key that only shows up in the console, so with the use of the pipe and `tee`<br/>
we can write the console output into a file. But we also need the public key, which we do by also piping it with `wg pubkey`, which takes the<br/>
private key and with that makes the public key, we write it in a file with the `>` operator commonly used in UNIX shells.

&copy; 2022 [manuals contributors](https://github.com/thefirethirteen/manuals/blob/main/contributors.md)
<br/> Licensed under the [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) license

<br/> Needs completion - 20.07.2023
