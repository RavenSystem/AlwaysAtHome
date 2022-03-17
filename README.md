# AAH - Always At Home

[![Donate](https://img.shields.io/badge/donate-PayPal-blue.svg)](https://paypal.me/ravensystem)

[![Twitter](https://img.shields.io/twitter/follow/RavenSystem.svg?style=social)](https://twitter.com/RavenSystem)

[![Chat](https://img.shields.io/discord/594630635696553994?style=social)](https://discord.gg/v8hyxj2)

VPN solution based on IPSec IKEv2 for Apple devices.

## Installation on Asus-Merlin routers

[Asus-Merlin Firmware](https://www.asuswrt-merlin.net)

### 1. DDNS

Setup a DDNS service to access to your public IP address from Internet using a hostname.

In router web, go to `WAN -> DDNS` and configure as needed.

If Asus router is not connected directly to Internet, you must select `External` for `Method to retrieve WAN IP` and UDP-4500 port to it.

### 2. IPSec Setup

Enter to router using SSH access, and exec following command:

```shell
curl -o /jffs/scripts/ipsec.postconf https://raw.githubusercontent.com/RavenSystem/AlwaysAtHome/main/ipsec.postconf && chmod a+x /jffs/scripts/ipsec.postconf
```

### 3. Configure VPN users

In router web, go to `VPN -> VPN Server -> IPSec VPN`:
- Set `Enable IPSec VPN Server` to `ON`.
- At bottom, create all users with their passwords, using `+` button, and selecting `V1&V2` for `Supported IKE version`.
- When finish, click on `Apply`.

## iOS/iPadOS/macOS Installation

