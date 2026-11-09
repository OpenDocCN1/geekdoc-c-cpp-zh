
| SSID | TOTAL | PERCENT |
|---|---:|---:|
| ZyXEL | 34,749 | 0.123 |
| FreeWiFi | 34,536 | 0.122 |
| (null) | 32,797 | 0.116 |
| Philips WiFi | 31,534 | 0.112 |
| honorss | 29,894 | 0.106 |
| Neuf WiFi | 29,254 | 0.104 |
| tsunami | 28,927 | 0.103 |
| tmobile | 28,766 | 0.102 |
| FRITZ!Box Fon WLAN 7170 | 28,328 | 0.100 |
| Guest | 26,960 | 0.096 |
| 101 | 26,886 | 0.095 |
| orange | 26,155 | 0.093 |
| 3Com | 25,253 | 0.089 |
| orange12 | 24,595 | 0.087 |
| attwifi | 22,066 | 0.078 |
| USR8054 | 22,009 | 0.078 |
| Linksys-g | 21,923 | 0.078 |
| SFR WiFi Public | 20,318 | 0.072 |
| Wayport Access | 20,180 | 0.071 |
| orange14 | 18,236 | 0.064 |
| eduroam | 17,602 | 0.062 |
| HomeNet | 16,299 | 0.058 |
| WLAN-AP | 15,098 | 0.053 |
| FRITZ!Box Fon WLAN 7113 | 14,532 | 0.051 |
| Customer ID | 14,457 | 0.051 |

Source: WIGLE.net (www.wigle.net/gps/gps/main/ssidstats)

As you can see from Table 10-3, the second most popular SSID was Linksys, which shows an astounding 1,968,509 units found, and Linksys-G had 21,923 units found to date by wardrivers, or 7 percent of all the devices found.

What you can take away from this is that changing or hiding the SSID of your unit is vital for proper wireless security.

## Reducing Power Output of a WAP

Many gadgets that people use every day are essentially radios (such as the car radio, satellite radio, cell phones, smartphones, Bluetooth system devices, and more). As you have learned in this chapter, your Wi-Fi router or WAP is a radio.

Radio transmitters are measured in broadcast strength (that is, the amount of power they can output). It’s measured in milliwatts, watts, or megawatts (as is the case with your terrestrial car radio). The higher the power (or wattage), the farther the signal will travel. If your Wi-Fi signal can leave your premises through a window or other exit point, a directional antenna like the Yagi can gather up enough of the signal to use it.

One feature that many modern routers support is reducing the power output. Sometimes this is marketed as a “green” approach, but, in reality, it really has nothing to do with the environment. The lower output reduces the strength of the wireless signal and, therefore, lowers the range it will travel with any effectiveness. Although this may fall into the “security by obscurity” category, this feature can be beneficial to safeguarding your wireless network.

To determine whether your wireless router provides this capability, look for one of the following at your router’s admin setting:

- RF POWER
- TX POWER
- Lower broadcast power

These generic terms are often used by manufacturers to indicate the product provides the capability for you to reduce power output.

> **NOTE** Be careful about manufacturers’ claims for some equipment. Some routers and WAPs may be marketed with the claim that they allow lowering of the power output, but you may discover that they do not. Check with the manufacturers’ websites to verify. Additionally, if the manufacturers offer any live sales assistance, you can pose the question via that method.

If you have a high-output router, consider locating it as far into the center of your building as possible. Also, ensure that your transmission range is kept to a minimum. In other words, if you can walk across the street with your laptop computer in hand and connect to your wireless network, then the signal emanating from your wireless network is too strong.

## Wireless Security Tools

To better understand how to solve issues identified by your threat matrix, you should understand some of the tools available to the bad guys who want to

**Table 10-4 (continued)**

| TOOL | DESCRIPTION |
|---|---|
| airdecloak-ng | Removes WEP cloaking from a packet capture file |
| airdriver-ng | A script that provides information and allows installation of wireless drivers |
| airdrop-ng | A rule-based wireless de-authentication tool |
| aireplay-ng | Injects and replays wireless frames |
| airgraph-ng | Graphs wireless networks |
| airmon-ng | Enables and disables the monitor mode on wireless interfaces |
| airodump-ng | Captures raw 802.11 frames |
| airolib-ng | Precomputes WPA/WPA2 passphrases in a database to be used with aircrack-ng |
| airserv-ng | A wireless card TCP/IP server that allows multiple applications to use a wireless card |
| airtun-ng | Creates a virtual tunnel interface |
| easside-ng | An auto-magic tool that enables communication to a WEP-encrypted access point without knowing the key |
| packetforge-ng | Creates various types of encrypted packets that can be used for injection |
| tkiptun-ng | Injects a few frames into a WPA TKIP network with QoS |
| wesside-ng | An auto-magic tool that incorporates a number of techniques to seamlessly obtain a WEP key in minutes |

As you can see, someone wanting to penetrate your wireless network has many tools at his or her disposal.

## Technical Countermeasures

For the highly paranoid, you can do some things to restrict your signals leaving your premises, such as turning off the wireless device or nailing up wire mesh to the walls and grounding it. However, if you need Wi-Fi, but want to be as secure as possible, choose a very modern device that supports the 802.11n protocol or newer. Choose a very strong and random password, and change it every 30 days or more often.

Devices are available to stop transmission of wireless signals, but these work in the same frequency range as cell phones and other devices. To use this type of device, you may want to mount it outside of your premises to kill any outgoing signals. There could easily be legal concerns in this case, as well. You should check with your attorney before using any device that alters transmissions, because this discussion is not offering a legal opinion.

These suggestions are included for educational purposes only and, of course, if you have this much of a concern, then not using wireless is the best alternative.

## Bluetooth Security Considerations

Bluetooth is the technology that allows users to make hands-free calls, use a wireless mouse and keyboard, and annoy people by talking into thin air using earpieces. Bluetooth is a compact “data” radio. It operates on an unlicensed frequency, and transmits at a maximum distance of 100 meters (109 yards). Figure 10-1 shows a typical Bluetooth setup.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_362_0.png)

In Figure 10-1, you can see the mobile phone, personal digital assistant (PDA), and laptop computer all being “paired.” Many laptops today support both Wi-Fi and Bluetooth, primarily because they can be packaged in a single chip. This enables the manufacturers to offer the most options at the lowest cost to you.

Bluetooth security has improved since its inception, and, for the most part, gone are the days of sitting on an airplane and using your laptop to connect to other laptops. This, of course, is rude, possibly illegal, and was a quite frequent practice in the early days of this standard.

Like most technologies, however, flaws have been discovered that have driven the development of new standards. Given its special role in your network, Bluetooth poses a very large potential threat to your website security. If a dedicated attacker can use Bluetooth to gain access to your systems, desktops, or your network, then planting a virus to gain your passwords is a simple matter. Yet, despite the downsides, Bluetooth can be a useful technology, and can be an effective tool, if you implement proper safeguards.

### Bluetooth Pervasiveness

Today, hundreds of devices depend on the Bluetooth standard. A brief search on the Internet reveals devices that are built for the following applications:

- Audio/visual
- Personal computers
- Mobile telephony
- Automotive
- Office equipment
- Audio (as in stereo equipment)
- Medical
- Home

Because this technology is so pervasive in our culture, the chances are good that you have it in your office. Again, the idea of this book is to prepare you for holistically protecting your CMS and infrastructure. You want to protect Bluetooth from any outside (non-authorized) activity at all costs. So, the following sections provide a look at a few security basics.

### Bluetooth Threats

If you include a dose of common sense when you use Bluetooth for your applications, you should have minimal problems. In fact, using Bluetooth offers major advantages. Yet, you must recognize and mitigate the risks. The technology and devices are susceptible to many of the same wireless threats that exist for WAPs.

Wireless devices (including those with Wi-Fi and Bluetooth technologies) can be susceptible to a classic “man-in-the-middle” attack or message modification. Unauthorized use of these devices can introduce even more threats.

Following are specific types of attacks identified by the National Institute of Standards and Technology (U.S. Commerce Department) in its guide to Bluetooth security:
