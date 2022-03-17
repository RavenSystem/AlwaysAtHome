# AAH - AlwaysAtHome

[![Donate](https://img.shields.io/badge/donate-PayPal-blue.svg)](https://paypal.me/ravensystem)

[![Twitter](https://img.shields.io/twitter/follow/RavenSystem.svg?style=social)](https://twitter.com/RavenSystem)

[![Chat](https://img.shields.io/discord/594630635696553994?style=social)](https://discord.gg/v8hyxj2)

VPN solution based on IPSec IKEv2 for Apple devices.

## Installation on Asus-Merlin routers

### 1. DDNS

Setup a DDNS service to access to your public IP address from Internet using a hostname.

In router web, go to WAN -> DDNS and configure as needed.

### 2. 

```shell
curl -o /jffs/scripts/ipsec.postconf https://raw.githubusercontent.com/RavenSystem/AlwaysAtHome/main/ipsec.postconf && chmod a+x /jffs/scripts/ipsec.postconf
```
