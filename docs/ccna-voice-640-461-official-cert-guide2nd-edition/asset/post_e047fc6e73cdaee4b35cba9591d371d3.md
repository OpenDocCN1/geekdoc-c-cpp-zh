
Figure 13-16 shows the LDAP Directory Configuration page.

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_400_0.png)

Figure 13-16 LDAP Directory Configuration Page

## Bulk Administration Import of CUC Users

Import users using the Bulk Administration Tool is a fast and easy way to create multiple-accounts if the required user information can be formatted as a CSV file. To import users, follow these steps:

1. Navigate to Tools > Bulk Administration Tool.
2. Under Select Operation, select Create. (Note that you can also Update, Delete, or Export.).
3. Under Select Object Type, choose Users With Mailbox.
4. Under Override CSV Fields When Creating User Accounts, select User Template Yes and select the desired Template.
5. Under Select File, browse to the .csv file that contains the user import information.
6. Specify a Failed Filename.
7. Click Submit.

**Note:** The formatting of the .csv is critical to the success of the import. The easiest way to get a correctly formatted file is to perform a BAT Export of a single user. The .csv file then has all the necessary information you need to create the import file correctly.

Select the user(s) you want to move, select the database to move them to, and click **Move Selected Mailboxes.**

## Chapter 13: Voicemail Integration with Cisco Unity Connection 373

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_402_0.png)

Figure 13-18 Edit Mailbox Store Page

## Message Aging Policy

The default Message Aging Policy deletes items in the Deleted Items folder after 15 days. To modify the policy, navigate to Message Storage > Message Aging Policy, and then select Default System Policy. (Note that you may create custom aging policies if you want.) You may disable the policy by deselecting the Enabled checkbox; the default is enabled. You may also choose to modify the following:

- Under Message Aging Rules Based on When the Message Was Last Modified, select whether or not to move New Messages to the Saved folder, and Saved Messages to the Deleted Items folder, and after how many days for each.
- Under the Secure Message Aging Rules Based on When the Message Was Created heading, you may choose to permanently delete secure messages or all secure messages that reach a specific age.

Figure 13-19 shows the Message Aging page for the Default System Policy.

## Mailbox Quotas

Setting mailbox size limits early in the deployment is a good idea. To begin, navigate to Message Storage > Mailbox Quotas. Here, you can change the System-Wide Mailbox Quotas, including the Warning, Soft, and Send/Receive thresholds. These quotas may be overridden in the User Template or individually per user.

Figure 13-20 shows the System-Wide Mailbox Quotas page.

## CCNA Voice 640-461 Official Cert Guide

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_403_0.png)

Figure 13-19 Messaging Age Policy

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_403_1.png)

Figure 13-20 System-Wide Mailbox Quotas Page

## Exam Preparation Tasks

## Review All the Key Topics

Review the most important topics in the chapter, noted with the key topics icon in the outer margin of the page. Table 13-3 describes these key topics and identifies the page number on which each is found.

Table 13-3 Voicemail Integration with Cisco Unity Connection Key Topics

| Key Topic Element | Description | Page Number |
| :--- | :--- | :--- |
| Paragraph | CUC integration with CUCM using SCCP | 347 |
| Paragraph | Call routing | 350 |
| Key Concept Box | CoS in CUC | 353 |
| Paragraph | Extension and call forward options | 355 |
| Paragraph | User creation options | 356 |
| Paragraph | Configure CUC end users | 365 |
| Paragraph | Importing end users in CUC | 367 |
| Paragraph | Importing users from LDAP | 368 |
| Paragraph | Bulk administration import of CUC users | 371 |

## Definitions of Key Terms

Define the following key terms from this chapter, and check your answers in the Glossary: integration, call handler, class of service (CoS), Administrative Extensions for XML (AXL), call routing rules

This chapter includes the following topics:

- Describe Cisco Unified Presence Features: This section discusses Cisco Unified Unified Personal Communicator, its features, operating modes, and protocol utilization. The basic capabilities of the Cisco Unified Communications Manager IP Phone Service and IP Phone Messenger are also reviewed.
- Describe Cisco Unified Presence Architecture: This section identifies the protocols and interactions associated with CUPS integrations to other Unified Communications applications and features. Cisco Unified Personal Communicator call flows in both desktop and softphone mode are described, along with regulatory compliance and QoS considerations.
- Enabling Cisco Unified Presence: This section reviews the steps required to configure end users so that they can use Cisco Unified Personal Communicator in either desk phone control mode or soft-phone mode.

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_405_0.png)

## Enabling Cisco Unified Presence Support

Cisco Unified Presence Server (CUPS) extends the native Presence capabilities of Cisco Unified Communications Manager to include multiple communications methods and status, as well as important enterprise features relating to compliance with legislation regarding retention of communications. This chapter introduces CUPS and briefly describes some of the implementation considerations in its deployment.

## “Do I Know This Already?” Quiz

The “Do I Know This Already?” quiz allows you to assess whether you should read this entire chapter or simply jump to the “Exam Preparation Tasks” section for review. If you are in doubt, read the entire chapter. Table 14-1 outlines the major headings in this chapter and the corresponding “Do I Know This Already?” quiz questions. You can find the answers in Appendix A, “Answers Appendix.

**Table 14-1** “Do I Know This Already?” Foundation Topics Section-to-Question Mapping

| Foundation Topics Section | Questions |
| :--- | :--- |
| Describe Cisco Unified Presence Features | 1–6 |
| Describe Cisco Unified Presence Architecture and Call Flows | 7–8 |

1. CUPS uses standards-based protocols for call control signaling and Instant Messaging. Which of the following are protocols used by CUPS for these purposes? (Choose two.)

- a. SCCP
- b. SSH
- c. SIP/SIMPLE
- d. XMPP

d. Multiple CSF clients can be installed on a single workstation, enabling simultaneous cross-platform communications.

6. Group Chat is a feature of CUPS. If chat rooms and discussions need to be available for future reference after all participants log off, which two steps are required?

- a. Obtain additional licenses for Persistent Chat.
- b. Install a WebEx server to record group chats.
- c. Install a third-party IM-retention compliance application on the CUPS server.
- d. Enable Persistent Chat on the CUPS server.
- e. Provision a PostgreSQL-compliant external database.

7. What components are required for CUPS to operate if the user is traveling?

- a. CSF registers with SIP.
- b. User account with CUCM using CTI.
- c. CUPC downloads config file from TFTP.
- d. CSF must be installed on the client.

8. How can calendar information in Outlook be integrated into CUPS so that Presence status?

- a. Using WebDAV
- b. Using SIP/SIMPLE
- c. Using CTIQ
- d. Using XMPP

## Foundation Topics

## Describe Cisco Unified Presence Features

Cisco Unified Presence Server (CUPS) extends the native Presence capabilities of Cisco Unified Communications Manager to include multiple communications methods and status, as well as important enterprise features relating to compliance with legislation regarding retention of communications. This chapter introduces CUPS and briefly describes some of the implementation considerations in its deployment. The primary goal of CUPS is to reduce communication delays by providing instant and useful information about the capability and availability of contact. Users can indicate whether they are available, and by methods, including desk phone, mobile phone, or conferencing application. This signaling capability can be extended to applications to allow contact with the right individual to be quickly established. This helps resolve support or customer issues more quickly, eliminating phone tag and the delays associated with e-mails.

CUPS is tightly integrated with CUCM, which provides central control and Native signaling (on-/off-hook status). CUPS provides a central collection point for user capabilities and status by way of standards-based signaling using Session Initiation Protocol (SIP), SIP for Instant Messaging and Presence Leveraging Extensions (SIMPLE), and Extensible Messaging and Presence Protocol (XMPP). A variety of client interfaces are available, including Unified Personal Communicator (CUPC), which provides a rich and tightly integrated user experience.

## Cisco Unified Personal Communicator

CUPS provides a single interface for the most commonly used Communicator tools. From the CUPS application, users can initiate voice calls (either through deskphone or softphone mode). Contacts are listed with their enhanced Presence status, providing click-to-communicate functionality by phone call, video call, chat, group, chat, and collaboration interaction with a simple interface to transition from one medium to another. Chat is enabled using the Jabber Extensible Communications Platform (XCP) using XMPP as the chat protocol.

## CUPC Operating Modes

CUPC operates in two modes:

- Desktop phone mode: CUPS can control the user's desk phone to place calls. The IP phone must be registered with CUCM and associated with the user. CUPS uses Computer Telephone Integration Quick Buffer Encoding (CTIQBE) for IP phone control. Figure 14-1 illustrates the protocol interaction when CUPS is in desktop mode.
