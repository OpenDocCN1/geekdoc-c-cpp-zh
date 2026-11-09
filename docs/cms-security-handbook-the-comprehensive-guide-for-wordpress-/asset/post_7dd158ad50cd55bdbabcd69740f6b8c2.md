
As you can see, this matrix results in a score of “5” in the “High” category, and, thus, this fictional setup is at a high risk of being breached.

Depending on your business, you will obviously design a different threat matrix. For example, if you are in a medical business in the United States, the requirements of the Health Insurance Portability and Accountability Act (HIPAA) and the more stringent requirements of the Health Information Technology for Economic and Clinical Health (HITECH) Act appear in your threat matrix. Another area of concern might be financial data, such as credit or debit card transactions. In the last few years, one high-profile retailer was breached through a wireless system, and millions of card numbers (and dollars) were stolen.

Design your threat matrix in the context of your situation, and follow up on the issues found as soon as possible. Just identifying the threats is only part of the battle, however. You should also understand some of the sources of those threats. The following sections take a look at some common sources.

## Misconfiguration

Misconfiguration is a simple, and oft-repeated, mistake. Invariably, it results from opening the box, turning on the device, plugging it in, and walking away.

Leaving default settings on any new device (especially a wireless device) is the equivalent of a misconfiguration. Wi-Fi routers running wide open with default settings are a simple target that deserves to be hacked. Always take the time to change the default settings.

To drive this point home, Table 10-2 shows the default usernames and passwords for some Wi-Fi routers and devices. Lists such as these are maintained publicly on the Internet, and are easy to find. Being armed with this allows attackers to attempt to log in to your Wi-Fi router. If they are successful, then that hole would allow them into your network. They could add their machine’s MAC address, authorizing them to be on the network. They could also change the settings and deny service, or perform any number of other malicious acts.

Information such as this can also be used as a defense. You can use this information to see whether your wireless device is configured to use the defaults, which you can then change to protect your wireless infrastructure.

As discussed in Chapter 1, a weak password is literally the weakest link in your security chain — specifically weak passwords that are easily guessed.

Weak passwords are a misconfiguration because they are easy to break. Because many wireless systems do not block multiple attempts, a weak password will be quickly compromised.

You must have a strong password for your systems. If you don’t, the common (and often fruitful) technique of brute-force cracking will result in a hacker easily obtaining access to your systems.

### Table 10-2: Default Usernames and Passwords for Wireless Devices

| MANUFACTURER | PRODUCT NAME | USER ID | DEFAULT PASSWORD | USE |
|---|---|---|---|---|
| D-Link | DCS-1000 | (none) | none | Internet camera |
| D-Link | DI-524 | admin | none | Wireless broadband router |
| D-Link | DI-614+ | user | (none) | 2.4GHz (802.11B) wireless router |
| Linksys | WAP54G | (none) | admin | Wireless G access point |
| Linksys | WRT110 | admin | admin | Wireless router |
| Linksys | WRT54GS | admin | admin | Wireless G access point with speed booster |
| SMC | None Needed | MiniAP |  | Wireless router |
| Netgear | WG302 | admin | password | 802.11G Wi-Fi access point |

This attack looks for common words found in wordlists. Following are some common default passwords found in a wordlist, which an attacker can easily use to compromise your wireless network:

- babygirl
- single
- 1234567890
- qazwsx
- pretty
- pokemon
- hottie
- iloveyou1
- teamo
- iloveyou2
- 987654321
- hahaha
- naruto
- poop
- spongebob
- blessing
- daniela
- blahblah
- princesa
- forum
- christ
- blink182
- Blessed
- 123qwe

This example represents a very small sample of one of the many hundreds of thousands of wordlists out there. Obviously, weak passwords such as these are easy to crack. It’s simply a matter of checking to see if your passwords (or close variations of them) are available by performing an Internet search.

## Dealing with Rogue Wireless Devices

In Chapter 1, you learned about WiFiFoRum, which is a handy software tool that allows you to see and log all the wireless devices in its range. One way to use this tool is to perform an initial sweep of your environment to determine what is there and what should not be there. Deal with those WAPs that should not be there (sometimes known as *rogue devices*) by disabling them, removing them, or securing them.

Disabling rogue WAPs is strictly a policy decision. If your policy states that only your technical staff can deploy Wi-Fi, then any wireless devices attached to your network should be considered rogue devices.

Another device is the pocket Wi-Fi detector. Several different brands are available.

Using one of these tools provides the capability to quickly sweep an area for wireless devices. If they exist, they will show up. WiFiFoRum gives you a good directional finder to locate the occasional under-the-desk wireless device.

Typically, a wireless device that has been sneaked into your network will not conform to your security standards, thus becoming an easy target for hackers.

The frequency you should check for rogue devices is based entirely on your environment. If you have only a few employees, then you should be fine with checking only once in a while. If you have a very large environment, you’ll need to consider a more frequent scan.

## People

People are clearly the means by which a threat happens. However, if you were to categorize those evildoers, they would fall into two groups:

- *Internal* — This category includes employees or contractors. These people have easy and authorized access to your premises and your wireless network. An employee may foolishly share a Wi-Fi key, or may install Firesheep or another session hijacking tool to exploit the network.
- *External* — This category includes those who want to break in and, of course, the person randomly looking for wireless networks to exploit. These people may be in possession of a stolen device that has a wireless access key on it. Although this key may be encrypted, utilizing the device to gain access to the wireless network is possible.

Your best bet is to define a strong policy to deal with the “people” threat.

## Mapping Systems

Part of a dedicated hacker’s standard fare is to map your environment. This job requires different tools for different parts of the network.

Mapping the wireless portion of your infrastructure requires a number of tools that are freely available, including the following:

- *Wireless Geographic Logging Engine (WiGLE)* — The `www.wigle.net` website provides a wealth of regularly updated information, such as the 26,969,388 WAPs that had been reported as of this writing. This, by the way, came from 1,154,921,792 unique observations — that’s right, more than 1 billion. Today, this sport or hobby (or whatever you want to classify it as) continues to look out for WAPs, both open and closed.
- *Seattle Wireless* — Another link that provides a well-documented guide and source of parts to build an antenna is Seattle Wireless, located at `www.seattlewireless.net/index.cgi/AntennasHowTo`.
- *LeWi-Fi* — This tool (located at `http://code.google.com/p/lewifi/`) is a floor plan mapper that enables an attacker to map where the Wi-Fi signals are, their names, and so on.
- *General Defense* — The `www.wardrive.net/general/antenna/` website provides the hobbyist and the hacker with a well-documented guide to Wi-Fi defense — and attack.

As you can see, the safe use of Wi-Fi is not simply a matter of turning on a Wi-Fi access point and going on about your day. It does require some preplanning to ensure that it’s secured.
