
10. ☑ D is correct. You should execute the srtp command in the dial-peer configuration mode.

☒ A, B, and C are incorrect. If the srtp command is used in the global voice service configuration mode, it will apply to all dial peers by default. You do not use the srtp command with either switch port interfaces or router port interfaces. The srtp command is only supported on dial peers and on the global voice service configuration mode.

## LAB ANSWER

You will not have to execute any commands on the switches. The switches will use Layer 2 forwarding and RTP as well as RTCP run on top of UDP, which is a Layer 4 protocol. The switches will simply forward on the RTP packets whether they use sRTP or standard unencrypted and unauthenticated RTP.

Because you want to enable sRTP by default, you should execute the srtp command while in global voice service configuration mode. This will enable sRTP for all dial peers by default. For dial-peer 650, you should execute the no srtp command while in the dial-peer configuration mode. This action will override the default settings coming from the voice service configuration.

![](img/ee67e6cd30f16bc39d653f87870eabb5_576_0.png)

## A

### About the CD

The CD-ROM included with this book comes complete with MasterExam, CertCam videos from the author, and an electronic version of the book. The software is easy to install on any Windows 2000/XP/Vista/7 computer and must be installed to access the MasterExam feature. You may, however, browse the electronic book and the CertCam video training directly from the CD without installation. To register for the bonus MasterExam, simply click the Bonus MasterExam link on the main launch page, and follow the directions to the free online registration.

### System Requirements

The software requires Windows 2000 or higher and Internet Explorer 6.0 or above and 20 MB of hard disk space for full installation. The electronic book requires Adobe Acrobat Reader.

### Installing and Running MasterExam

If your computer CD-ROM drive is configured to auto-run, the CD-ROM will automatically start up upon your inserting the disc. From the opening screen you may install MasterExam by clicking the MasterExam link. This will begin the installation process and create a program group named LearnKey. To run MasterExam, use Start | All Programs | LearnKey | MasterExam. If the auto-run feature did not launch your CD, browse to the CD and click the LaunchTraining.exe icon.

### MasterExam

MasterExam provides you with a simulation of the actual exam. The number of questions, the type of questions, and the time allowed are intended to be an accurate representation of the exam environment. You have the option to take an open book exam, including hints, references, and answers, a closed book exam, or the timed MasterExam simulation.

When you launch MasterExam, a digital clock display will appear in the bottom right corner of your screen. The clock will continue to count down to zero unless you choose to end the exam before the time expires.

### CertCam Video Training

CertCam avi clips provide detailed examples of key certification objectives in audio video format direct from the author of this book. These clips walk you step-by-step

![](img/ee67e6cd30f16bc39d653f87870eabb5_580_0.png)

## Glossary

- **access control** The prevention of access to resources by unauthorized users and systems.
- **access device** A common term for a networking device through which client devices connect to a network; for example, a typical access point device.
- **ad hoc network** An alternate term often used to reference an independent basic service set (IBSS) or a peer-to-peer network in a wireless LAN (local area network).
- **address signaling** The method used to transmit dialed digits on telephone networks. Dual-tone multifrequency (DTMF) is a common address-signaling system.
- **Advanced Encryption Standard (AES)** The encryption standard that replaced the Digital Encryption Standard (DES) in order to improve encryption strength. It is based on the Rijndael algorithm.
- **a-Law** A compressing and expanding (companding) algorithm used outside the United States and Japan.
- **Application layer** The layer of the OSI model (see OSI model) that provides access to the lower OSI layers for applications and provides information to applications from the lower OSI model layers. Also known as Layer 7.
- **area code** A three-digit prefix identifying the geographic region to which calls should be routed.
- **authentication** A process that results in the validation or invalidation of user or system credentials.
- **authentication server** A device that provides 802.1X authentication services to an authenticator in an 802.1X/EAP implementation.
- **authenticator** A device at one end of a point-to-point LAN (local area network) segment that facilitates the 802.1X authentication of the device at the other end in an 802.1X/EAP implementation.
- **bandwidth** Either the difference between the upper and lower frequencies used by a wireless channel, or the sheer amount of data that may be communicated through the channel including all framing protocol overhead, or sometimes the number of payload bits that can be communicated through the channel in a second—more properly called *throughput*.
- **B-channel** An ISDN bearer (B) channel that carries voice, video, or data.
- **binary** Data represented as 1’s or 0’s.
- **bit** An individual information element that can be equal to 1 or 0. A single bit can represent any two values to an application.
- **byte** A collection of bits. Usually 8 bits in computer systems.
- **call admission control (CAC)** A system that allows you to manage VoIP call volumes when quality of service controls are insufficient.
- **call agent** The component containing the call-forwarding logic in an MGCP network implementation.
- **call detail record (CDR)** A record of the details of a call including time, duration, and source.
- **capacity** The amount that can be contained or managed. System capacity is usually a measurement of storage space or data space. In communications systems, capacity is a reference to the amount of data that can be transferred through the system in a given window of time.
- **central office (CO)** A location including one or more PSTN switches. The CO may be connected with other telephone systems.
- **channel** An instance of communications medium (radio frequency bandwidth) used to pass information between two communicating stations (STAs).
- **circuit switching** A switching method used to reserve a route or path between the two endpoints that need to communicate.
- **cluster** In a Cisco VoIP network, a logical collection of call managers (Cisco Unified Communications Manager or Cisco Unified Communications Manager Express).
- **coaxial cable** Networking cable that is implemented with a center conductor made of copper surrounded by a shielding made of some type of plastic. Also known as coax.
- **codec** An abbreviation for coder/decoder. A method used to convert analog signals to digital signals and vice versa. Examples include G.711, G.729, and G.728.
- **contact center** A location or call center that processes PSTN, VoIP, e-mail, instant messaging, and other forms of customer contact.
- **convergence** The process of bringing voice, multimedia, and data communications together on a shared network.
- **core device** A common term for a networking device that neither connects to client devices nor provides services to the network other than packet forwarding.
- **coverage** A term used to refer to the physical space covered by an access point. An administrator might say that she needs to provide coverage in the Accounting department, meaning that she needs to be sure the RF signal from the access point is of acceptable quality in that physical area that contains the Accounting department.
- **Data Link layer** The layer of the OSI model (see OSI model) that is responsible for physical network management such as the detection of errors in the physical media and for locating and transferring data on the physical medium such as Ethernet. This is where MAC frames and data reside. Also known as Layer 2.
- **data rate** The rate at which bits are communicated in a WLAN during a single frame transmission. In a wired LAN, it is the rate at which bits are communicated. This rate may vary in a WLAN.
