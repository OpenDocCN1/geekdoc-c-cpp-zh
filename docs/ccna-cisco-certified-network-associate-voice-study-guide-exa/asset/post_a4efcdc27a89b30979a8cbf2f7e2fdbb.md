
### System Parameters

On the System tab, you can configure the regional settings, which impact call tones, phone languages, date and time format, and the voice mail language. You may also configure system-wide speed-dial settings here.

### Network Parameters

The configurable network parameters include the IP information for the UC500 device and the VLAN information. Much like SOHO routers (such as Linksys and D-Link devices), the UC500 series offers simple configuration of DHCP servers and the IP address of the call manager (the CME in the Cisco world). The following parameters can be configured on the Network tab of the Devices dialog box:

- **VLAN Number** This can be a number from 1 to 1001. This is the VLAN that will be configured as the voice VLAN.
- **DHCP IP Address Pool** This defines the range of addresses to be configured automatically for the clients. Supporting fields include the Subnet Mask, Exclude Address From, and To fields. The DHCP IP Address Pool field will contain the subnet identifier, for example, 192.168.1.0. The Subnet Mask field will contain the appropriate mask for the subnet identifier, for example, 255.255.255.0. The Exclude Address From and To fields will include the beginning and ending addresses that define the range that should not be given out by the DHCP server, such as 192.168.1.50 to 192.168.1.59.
- **CME IP Address** This is the IP address of the Communications Manager Express (CME) call manager server. The supporting field is the Subnet Mask field used to identify the network on which the CME server resides.

### Auto Attendant and Voice Mail

Several fields can be configured on the AA & Voicemail tab. The sections to be configured include Auto Attendant, Script Parameters, and Voicemail. In the Auto Attendant section, you can configure the phone extension of the Auto Attendant service. This is usually the main extension phone number for the organization. You can also configure the outside number (the PSTN number) used to reach the Auto Attendant. Finally, you can use the default AA script, or select a custom script you've developed.

The Script Parameters section is not used if the default AA script is selected. When a custom script is selected, you can specify the audio file to play when the different keypad numbers are pressed. The numbers 0 through 9 can be configured. The Voice mail section lets you configure the extension and PSTN number dialed to reach the voice mail system.

**Exam Watch:** Remember that you can configure the audio file to play for the keypad presses of 0 through 9 in the AA & Voice mail tab of the Devices dialog box and that these options only apply when a custom or non-default AA script is used.

### SIP Trunks

If you are using analog connections to the PSTN through FXO ports or digital lines, you will not configure a SIP trunk. If you are using an Internet Telephony Service Provider (ITSP), you will need to configure a SIP trunk to the ITSP. To configure a SIP trunk on the SIP Trunk tab in the Devices dialog box, configure the parameters provided by your ITSP. The most current UC500 series software and CCA at the time this book was written offered support for the following service providers:

- AT&T
- Broadview
- British Telecom (BT)
- Cbeyond
- Covad
- Fibernet
- Nuvox
- One Communications
- PAETEC
- XO Communications

**Exam Watch:** Because service providers come and go, you will not be required to memorize this list of service providers for the 640-460 exam.

### Voice System Features

The Voice Features tab includes the ability to configure the following parameters:

- **Music on Hold** Simply select the audio file you want to play for MoH.
- **Intercom** Phones can be enabled for intercom use if the Enable Intercom check box is checked.
- **Paging** Paging groups can be enabled with three directory numbers (DNs) in each of a maximum of four paging group extensions.
- **Hunt Group** Hunt groups can be enabled with a timeout value, which indicates the number of rings to try for each number in the hunt group. The hunt type can also be specified. The hunt types include sequential, longest idle, and peer. A sequential hunt type sends the call to the first DN in the hunt group and only moves on to the next DN if the first does not answer in the timeout window. A longest-idle hunt type sends the call to the DN that has been idle for the longest time (not on a call for the longest time). A peer hunt type sends the call to the next DN in the hunt group after the DN that most recently answered a call (round robin).
- **Group Pickup** Group Pickup can simply be enabled here. Once enabled, a user can enter a code on his phone in order to answer someone else's phone in the same pickup group. Once Group Pickup is enabled, up to eight pickup groups can be specified.
- **Caller ID Block Code** This setting specifies the number a user must dial before dialing another number to block her caller ID. The caller ID block number will be preceded by a \* when dialed by the user.
- **Outgoing Call Block Number List** This list includes numbers you do not allow internal users to dial.
- **Call Park** Call parking allows the user to place a call on hold and resume the call from another phone. Call park slots are configured to work on special extensions.
- **Multi-party (Ad hoc) Conference** Up to eight conference calls with up to three participants each are supported by default. Additionally, all callers must use G.711 or G.729 to reduce processing costs. However, you can enable mixed mode here if the DSP resources are available. Mixed mode allows a mixture of G.711 and G.729 users in the conference at the same time.

**Exam Watch:** **Remember the three hunt types configurable in the CCA:** sequential, longest idle, and peer. Also be sure to remember how they work. Sequential hunt types simply ring the first number in the list and try the next until a number answers.

**Longest idle** always rings the number that has not been on a call for the longest time. **Peer** always rings the number in the hunt group that immediately follows the number most recently answering a call.

### Dial Plans

The Dial Plan tab allows you to set up the dial plan to use on your VoIP network. You can set up several dial plan parameters, including:

- Extension digit length
- Outgoing call numbering plan
- Length of area codes
- Length of local external numbers
- Digit or digits required to place long-distance calls
- Requirements for placing international calls
- Access code number for outbound call placement
- Emergency number configurations
- Processing for inbound FXO calls
- Direct Inward Dial (DID) configuration

### User Parameters

The Users tab is used to create both users and phones. Simply clicking the New button gets you started in the process. You can specify the MAC Address, phone type, primary DN (extension), user first name and last name, user ID, password, and phone-specific settings.

*The CCA interface is subject to change. When this book was written, the tabs and options were available as defined here. However, you should check the Cisco web site for documentation on the most recent version of the CCA to ensure you understand where and how to configure these options in the version you are using.*

## CERTIFICATION OBJECTIVE 1.0.02

### 640-460: Implement Voice Mail Features Using Cisco Unity Express

The Cisco Unity platform is the voice mail and messaging solution Cisco offers. It comes in many different editions, but for the 640-460 exam, you'll need to understand the basics of the Cisco Unity Express 640-460 edition. In this section, you will learn about the Cisco Unity Express hardware options and the basic configuration settings available within the system.

### Introducing Unity Express

Cisco Unity Express (CUE) is the small business edition of Cisco's voice mail and messaging solution. CUE provides voice mail services for up to 250 users in most implementations. You can use the command-line interface (CLI) or the GUI for management of the CUE modules and services. To fully understand CUE, you'll need to learn the following:

- Unity Express hardware implementations
- Features of Unity Express

### Unity Express Hardware

The CUE hardware comes in three basic versions:

- **AIM-CUE** This form factor uses the daughter card format and a flash memory module for the Linux file system and the message storage. The AIM-CUE version supports up to 50 mailboxes, six voice sessions, and a total of 14 hours of mailbox storage.
- **NM-CUE** This form factor uses the network module format and is shown in Figure 10-10. A hard drive is used for the Linux file system and the message storage. Up to 100 mailboxes can be created with eight voice sessions and 100 hours of mailbox storage.
- **NM-CUE-EC** The extended capacity of the NM-CUE version adds support for up to 250 mailboxes, 16 voice sessions, and 300 hours of mailbox storage.
