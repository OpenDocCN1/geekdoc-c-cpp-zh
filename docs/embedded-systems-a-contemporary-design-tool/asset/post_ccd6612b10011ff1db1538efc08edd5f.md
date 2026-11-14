
## Authentication

Moving inside the system, trusting incoming data, the access attempt, and trusting the sender are the next issues.

## TCP Three-Way-Handshake

The three-way-handshake protocol is used by transmission control protocol (TCP) to establish and setup a connection between two participants over an IP-based network. One participant is considered a client and the other a server; both share a secret key that we identify as ck for client key and sk for server key.

According to the protocol, a connection between two hosts is established in three steps: it is the three-way-handshake.

The client, who wishes to establish a connection, will:

- Select a random number Nc.
- Encrypt Nc using ck: E(Nc, ck) -> enc
  Nc is now encrypted.

Send a SYN or synchronize packet with the encrypted random number, enc, and the client id to the server.

The server receives the message and responds:

- Decrypt enc: D(enc, sk) -> dec
  Received number is now decrypted.
- Compute dec -> dec + 1
- Encrypt dec + 1 using sk: E(dec+1, sk) -> encdec+1
  dec + 1 is now encrypted.
- Select a random number Ns.
- Encrypt Ns using sk: E(Ns, sk) -> ens
  Ns is now encrypted.

Send a SYN-ACK or synchronize-acknowledge packet with encdec+1 and the encrypted random number ens to the client.

The client receives the message and responds:

- Decrypt encdec+1 : D(encdec+1, sk) -> dec + 1
  Received number is now decrypted.
- If decrypted number matches the Nc + 1, the server is confirmed.
- Decrypt ens: D(ens, ck) -> dens
  Received number is now decrypted.
- Compute dens -> dens + 1
- Encrypt dens + 1 using ck: E(dens+1, ck) -> edens+1
  dens + 1 is now encrypted.
- Send an ACK or acknowledge packet with edens+1 to the server.
- The server receives the message.
- Decrypt edens+1 : D(edens+1, sk) -> dens + 1
  Received number is now decrypted.
- If decrypted number matches the Ns + 1, the client is confirmed.

## Digital Signatures

Trusting the data is the next issue. Trusting the data is partially addressed using digital signatures, which are a mathematically based scheme for verifying the legitimacy of digital data. The Digital Signature Algorithm (DSA) was developed by NIST, the National Institute of Standards and Technology. Such signatures are a routine component of typical cryptographic protocols. The objective of the digital signature is to authenticate the source, verify that the message was from the alluded source even if denied, and confirm that the message had not been altered in transit. To accomplish its verification task, the scheme utilizes three algorithms also known as (GSV) – Generate, Signing, Verifying.

### Generate, Sign, Verify

Key Generation. Randomly select a private key, prk, from an available set of such keys and return the private key (prk) – public key (puk) pair.

Signing. Generate a digital signature (disig) given a signature algorithm (SA), a digital message (DM), and a private key (prk). SA(DM, prk) → disig

Send the signed message with signature. Receive the signed message with signature.

Verify. For the given received message (RDM), public key (puk), signature (disig) and signature verification algorithm (SVA), accept or deny the message. Does SVA(RDM, puk) not equal or equal RDM?

## Digital Certificate

### nonrepudiation

The final step is confirming the message source, i.e. the owner of the public key. This is known as nonrepudiation. Here we are looking to ensure, with high confidence, that the data and the source of the data are genuine and legitimate.

### Digital Signature certificate issuer

Such assurance can be accomplished through an electronic Digital Certificate that is used to prove the identity of the key owner. The certificate includes information about the owner of the certificate and the digital signature of the certificate issuer that has verified the digital certificate’s contents.

- Guarding the Keys to the Henhouse

The approaches to securing the system frequently depend upon secret keys that are typically stored in the system. However, if these keys are lost or broken, the embedded system can potentially be compromised. Consequently, security measures must be established within the system, and those measures must ensure that the keys are secure. Any attempts to compromise that security must be prevented. As mentioned earlier, the secure key(s) must be kept inside of a secure device that is itself protected by a combination of hardware and software systems that must be able to subvert any unauthorized access attempts. Once again, such a device is often referred to as a Secure Operations Center (SOC) or TrustZone. A high-level diagram of such a device is given in Figure 8.44.

Unlike a physical key, the secure keys are a pattern of binary bits and are typically held in a Secure ROM similar to secure data held on a person’s passport. That ROM must, therefore, be held in the SOC.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_458_0.png)

When needed, such keys need to be transferred to RAM where they can be used to support outside world information exchange. Like the data transfer from a passport when checking onto an aircraft, the Secure ROM to RAM transfer occurs in clear text. If the transfer is affected over a system bus in clear text, then during that time data compromise is possible. To mitigate such a possibility, the RAM should be implemented in the SOC. A similarly secure boot loader should ensure that the system executes a clean boot of all of the proper and legitimate firmware and that any attempts to alter or defeat the boot loader should be blocked.

The keys stored in the ROM can also be encrypted. However, the keys to the encryption of the secret keys now have to be held somewhere and protected and the problem repeats. Limited and controlled access to the SOC and enclosed memories and a task assigned to the memory management unit (MMU) can help; however, the probability that ultimately someone can defeat the protection exists. The goal should be to make that process as difficult and complex as possible.

In Chapter 14, we discuss a power management technique called Power Gating, in which the power to designated subsystems is lowered or turned off during passive periods to aid in reducing system power consumption. Care must be taken when using such a technique. If the trust zone is included in the set of subsystems for which the power can be controlled, then it becomes vulnerable to side channel attacks. If the technique is employed, then the trust zone, at the minimum, should be segregated and managed by a separate system in a manner similar to that discussed earlier in this chapter under fail operational capability.

## 8.23.5 Firewall

### denial of service attack

Taking an external view of an embedded system, a denial-of-service attack is an attack on a system initiated with the intent of diverting or preventing it from performing its intended job. Such an attack typically commences by flooding targeted machine or resource with superfluous requests, potentially from a wide variety of sources, in an attempt to overload the system and prevent some or all legitimate requests from being fulfilled.

### firewall

A basic firewall, illustrated in Figure 8.45, is a tool that can help to handle and mitigate such attacks. In the context of embedded systems, the firewall is considered to be host-based and comprises a layer of software on the system that monitors and controls traffic into and out of the system.

Fundamentally, in this context, the firewall is a router or set of routers and a filter that act, in concert, as a gatekeeper to screen network traffic between the Internet and a trusted and secure local site. The device utilizes a set of security rules to manage and control traffic into or out of the secured device.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_459_0.png)

In the diagram, the two routers apply those rules to every incoming and outgoing packet. For example, the routers may block all incoming network packets directed to a particular IP address or TCP port, thereby protecting the secure device from a flood of packets. The gateway views the packets from an application perspective. The gateway analyzes each message according to sets of specified criteria and rules, then decides whether to accept, transmit, or discard a message. Thus, the only traffic allowed into or out of the system is that specified in the access policy and security rules. To facilitate the aforementioned goal of forestalling any successful attack to the distant future, we can introduce another interpretation of the term “firewall.” In the larger sense, a firewall is essentially a barrier, designed and installed with the intention of preventing undesired events from intruding into a protected area. Building on the MILS model discussed earlier, rather than a single firewall protecting access to a protected area, implement a cascade of firewalls, each with a different protocol that must be ultimately followed to gain access to the trusted area. With such a scheme, an attack that compromises/breaches one impediment will not be immediately successful and, if detected, can raise an alert to the system.

## 8.24 CLOSURE

Given the growing number of attacks on embedded systems, and following the guidelines discussed in this chapter, we conclude with a few simple words. First, backup, potentially replicate, and isolate the most critical and essential parts of the system. Then, be prepared. Extend and support that preparation with a plan of action put together which anticipates that an attack might occur. Second, if such an attack does occur, quickly initiate an assessment of the situation and the extent of the damage. Third, try to limit and minimize any additional damage.

## 8.25 TOMORROW

Current research and successes in the AI areas of deep learning, supervised, unsupervised, and reinforced learning are showing significant progress in solving complex problems. These tools are showing great promise and potential as aides in recognizing and repelling attacks on embedded systems. They are also showing the same potential as weapons for initiating and conducting such attacks. The tools and methods that we have discussed in this chapter have a limited lifetime. We need to be continually diligent in our efforts to ensure the security of our systems.
