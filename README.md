# AAH - Always At Home

[![Donate](https://img.shields.io/badge/donate-PayPal-blue.svg)](https://paypal.me/ravensystem)

[![Twitter](https://img.shields.io/twitter/follow/RavenSystem.svg?style=social)](https://twitter.com/RavenSystem)

[![Chat](https://img.shields.io/discord/594630635696553994?style=social)](https://discord.gg/v8hyxj2)

VPN solution based on IPSec IKEv2 for Apple devices.

Main goal of this solution is to use native Apple VPN IPSec IKEv2 support with AES128 and SHA256, and on-demand feature to connect to VPN server automatically.

Tested Asus routers:
- GT-AX6000
- RT-AX88U
- RT-AX58U
- RT-AC86U
- RT-AC5300

## Installation on Asus-Merlin routers

You need a router running a recent version of [AsusWRT-Merlin-NG Firmware](https://www.asuswrt-merlin.net) with `Administration -> System -> Enable JFFS custom scripts and configs` sets to `Yes`.

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
- Fill `Pre-shared Key` with any very strong pass-phrase. However, this field will not be used to connect to VPN Server.
- At bottom, create all users with their passwords (use very strong passwords), using `+` button, and selecting `V1&V2` for `Supported IKE version`. Use only alphanumeric characters to avoid compatibility issues with different code character sets.
- When finish, click on `Apply`.

It is not possible to connect more than one device using same user at same time.

## iOS/iPadOS/macOS Installation

In order to work with this VPN Server, a mobile profile is needed.

Download [AlwaysAtHome.mobileconfig template](https://github.com/RavenSystem/AlwaysAtHome/raw/main/AlwaysAtHome.mobileconfig)

You must edit template with a text editor, replacing these fields:
- AAH_USERNAME: VPN Username
- AAH_PASSWORD: VPN Password
- AAH_HOSTNAME: DDNS Hostname (Warning, it appears twice).
- AAH_MYWIFI_1, AAH_MYWIFI_2: SSID of WiFi networks where VPN is disabled. It is mandatory to add WiFi where this VPN Server is running.

It is possible to add more WiFi networks, addind more lines
```xml
<string>AAH_MYWIFI</string>
```

When finish, copy file to iPhone/iPad/macOS using AirDrop or similar, and install it from Settings.
