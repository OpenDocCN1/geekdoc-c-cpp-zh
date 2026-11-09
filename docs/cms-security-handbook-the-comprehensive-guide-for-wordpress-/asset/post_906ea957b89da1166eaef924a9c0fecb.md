
- *Bluesnarfing* — Bluesnarfing enables attackers to gain access to a Bluetooth-enabled device by exploiting a firmware flaw in older devices. This attack forces a connection to a Bluetooth device, allowing access to data stored on the device, and even the device’s international mobile equipment identity (IMEI). The IMEI is a unique identifier for each device that an attacker could potentially use to route all incoming calls from the user’s device to the attacker’s device. Rerouting phone calls could be a prank, or a nasty event. Consider upgrading to the most modern Bluetooth devices for telephony applications.

- *Bluejacking* — Bluejacking is an attack conducted on Bluetooth-enabled mobile devices, such as cellular telephones, smartphones, and PDAs. Bluejacking is initiated by an attacker sending unsolicited messages to a user of a Bluetooth-enabled device. The actual messages do not cause harm to the user’s device, but they are used to entice the user to respond in some fashion, or add the new contact to the device’s address book. This message-sending attack resembles spam and phishing attacks conducted against e-mail users. Bluejacking can cause harm when a user initiates a response to a bluejacking message that is sent with a harmful intent.

- *Bluebugging* — Bluebugging exploits a security flaw in the firmware of some older Bluetooth devices to gain access to the device and its commands. This attack uses the commands of the device without informing the user, allowing the attacker to access data, place telephone calls, eavesdrop on telephone calls, send messages, and exploit other services or features offered by the device.

- *Car Whisperer* — Car Whisperer is a software tool developed by European security researchers that exploits a key implementation issue in hands-free Bluetooth car kits installed in automobiles. The Car Whisperer software allows an attacker to send or receive audio from the car kit. An attacker could transmit audio to the car’s speakers, or receive audio (eavesdrop) from the microphone in the car.

- *Denial of Service (DoS)* — Bluetooth is susceptible to DoS attacks. Impacts include making a device’s Bluetooth interface unusable and draining the mobile device’s battery. These types of attacks are not significant, because the proximity required for Bluetooth use can usually be easily averted by simply walking away. This is a low threat to you, and could be just considered an annoyance.

- *Fuzzing attacks* — Bluetooth fuzzing attacks consist of sending malformed or otherwise non-standard data to a device’s Bluetooth radio, and observing how the device reacts. A device’s response being slowed or stopped by these attacks indicates that a serious vulnerability potentially exists in the protocol stack.

## Security Recommendations

You do not need to drop your entire Bluetooth device inventory to safeguard your infrastructure. Rather, here are a few common-sense items to help you stay on track:

- A well-formed information security policy (which you will learn more about in Chapter 11) is your friend. In that policy, define what devices and what type of information can be sent over Bluetooth. Remember, just because someone makes a Bluetooth-enabled coffee pot doesn’t mean you need to use it.
- Consider discontinuing the use of any older Bluetooth devices. The reasons for this is that later (2008 and beyond) models are more secure and have better encryptions. For example, the original (Class One) Bluetooth radios have a 100 milliwatt (mW) output. This means that anyone within 100 meters (109 yards) can pick up and attempt to attack the signal. Bear in mind that this is an estimate, because there are many other influential factors, such as the device itself, sun-spot activity, materials of the building, terrain, and much more. Don’t count on this number being one you can rely on in all situations.
- Ensure that any Bluetooth device used is changed from its default settings.
- If possible, turn down the power on the devices to reduce the transmission range.
- Use a very strong PIN or password (device-dependent).
- Set passwords on devices that have a Bluetooth connection in the event of loss or theft. In the event of loss or theft, users should decouple the device from the Bluetooth device.
- Set up Bluetooth devices to be *non-discoverable*. This practice prevents attackers from mapping out your network through them, or knowing the names of the devices.
- Your Bluetooth device likely supports some form of *link encryption*. Activate it, if it exists.
- If you have no need for Bluetooth on a notebook computer, turn it off. This helps save battery life and may prevent a machine from being compromised.
- If a Bluetooth device is not in use, it should be turned off. There is no reason to give someone a window of opportunity.

Although you can use many other tactics, these should suffice for most organizations.

## Summary

In this brief tour of wireless security, you were introduced to many concepts and possibly new ideas. You gained an understanding of threats to your wireless security, and how to build a threat matrix. You were introduced to various tools that can be used to secure or attack your Wi-Fi connection, and, of course, the danger of not changing default passwords.

You learned that you should use SSL with any wireless network. You also learned how to find information regarding activation of SSL for each CMS covered in this book.

This chapter exposed several key points to building out your secure infrastructure, and you learned about Bluetooth security countermeasures.

Chapter 11 shows you how to develop an information security policy.

## Information Security Policy and Awareness

Your information security policy is a document that describes how you will deal with specific information security situations. This could define what the acceptable use of your e-mail system is, or it might dictate whether you can read employee e-mail. Today, a good information security policy will cover the gamut of information, such as e-mail, Instant Messaging (IM), backup storage, and acceptable use of company resources (meaning desktops, notebooks, servers, Internet connection, and so on).

An information policy is built to guide the employee, as well as to protect you and your company from inadvertent problems. Often, the employee excuse of “we didn’t know” tends to work, and sadly, it forces you to document all of your policies. Although people tend to gloss over employee policies, the information policy document will serve to push the burden of responsibility back onto the employee or user community.

Your information security policy should cover the responsibility of each person. The information policy also should cover license information (such as if you find pirated software, what to do), as well as what can or cannot be plugged into your network, such as an outside notebook or any other unauthorized device.

Awareness also falls into the information security category. People are often unaware of what is going on around them. This is a “perfect storm” situation for a social engineer (that is, someone who uses specific social techniques to get past another person’s defenses). A classic social engineering technique is to call someone in the company and fool him or her into helping the caller by providing a password. Unfortunately, this method works very well. Training your staff in proper phone screening can help to avoid this issue.

This chapter covers two aspects of the information security spectrum. The first half of this chapter provides an in-depth view of the information security policy itself. Although you won’t find here a full written plan, the discussion can help guide you to developing your own. The second part of the chapter helps you to develop a strong defense against social-engineering techniques and takes a look at the situational awareness paradigm.

## Establishing an Information Security Policy

The information security policy can be a single document stating what is and is not acceptable concerning what information can be divulged to whom. It may also be a collection of policy documents. The purpose of the information security policy is to protect you and your business from harm caused by the actions of employees, contractors, customers, and others who violate the rules. Following are the particular policy areas examined in this section:

- Overall information security policy
- Internet use
- Remote access
- Acceptable e-mail use
- Instant messaging
- Social media network use

Although this list of examined topics is not exhaustive, it’s meant to get you started on the proper path. This section covers a basic framework for your information security policy. Take the time to discuss the information presented in this chapter with your staff as it relates to your business and technical needs.

To begin, let’s start with the overall information security policy.

### General Information Security Policy

The primary document you will create is the information security policy. This document is typically delivered to employees for acknowledgment and signature. Its scope covers the use of the company’s information resources.

The policy should be updated from time to time as your technology needs change. It’s important that the employees read the policy document and acknowledge an understanding of its contents by signature.
