# AAH - Always At Home

[![Donate](https://img.shields.io/badge/donate-PayPal-blue.svg)](https://paypal.me/ravensystem)

[![Twitter](https://img.shields.io/twitter/follow/RavenSystem.svg?style=social)](https://twitter.com/RavenSystem)

[![Chat](https://img.shields.io/discord/594630635696553994?style=social)](https://discord.gg/v8hyxj2)

VPN solution based on IPSec IKEv2 for Apple devices.

Main goal of this solution is to use native Apple VPN IPSec IKEv2 support with AES128GCM, and on-demand feature to connect to VPN server automatically.

## Installation on Asus-Merlin routers

[Asus-Merlin Firmware](https://www.asuswrt-merlin.net)

### 1. DDNS

Setup a DDNS service to access to your public IP address from Internet using a hostname.

In router web, go to `WAN -> DDNS` and configure as needed.

If Asus router is not connected directly to Internet, you must select `External` for `Method to retrieve WAN IP` and configure NAT UDP-4500 port to it, or DMZ.

### 2. IPSec Setup

Enter to router using SSH access, and exec following command:

```shell
curl -o /jffs/scripts/ipsec.postconf https://raw.githubusercontent.com/RavenSystem/AlwaysAtHome/main/ipsec.postconf && chmod a+x /jffs/scripts/ipsec.postconf
```

### 3. Configure VPN users

In router web, go to `VPN -> VPN Server -> IPSec VPN`:
- Set `Enable IPSec VPN Server` to `ON`.
- At bottom, create all users with their passwords (use very strong passwords), using `+` button, and selecting `V1&V2` for `Supported IKE version`.
- When finish, click on `Apply`.

It is not possible to connect more than one device using same user at same time.

## iOS/iPadOS/macOS Installation

In order to work with this VPN Server, a mobile profile is needed.

Download [AlwaysAtHome.mobileconfig template](https://github.com/RavenSystem/AlwaysAtHome/raw/main/AlwaysAtHome.mobileconfig)

You must edit template with a text editor, replacing these fields:
- AAH_USERNAME: VPN Username
- AAH_PASSWORD: VPN Password
- AAH_HOSTNAME: DDNS Hostname (Warning, it appears twice).
- AAH_MYWIFI_1, AAH_MYWIFI_2: SSID of WiFi networks where VPN is disabled.

It is possible to add more WiFi networks, addind more lines
```xml
<string>AAH_MYWIFI</string>
```

When finish, share file to iPhone/iPad/macOS, and install it from Settings.
