![](bbox=[0.085, 0.073, 0.615, 0.296])

# Figure 14-1 CUPC in Deskphone Mode

+   - Softphone mode: When the IP phone is not available or the user is away from his desk, CUPC activates the associated softphone based on the Cisco Unified Client Services Framework (CSF), which registers the softphone with CUCM as a SIP device (see Figure 14-2). The CUCM administrator must create the CSF device in order to enable this functionality.

![](bbox=[0.085, 0.49, 0.615, 0.706])

# Figure 14-2 CUPC in Softphone Mode

# Enterprise Instant Messaging

CUPC provides TLS-secured Chat and Group Chat capability. Ad-Hoc Group Chat sessions are stored in memory on the CUPC server. The Persistent Chat feature enables group chat rooms where the conversation persists even when all participants have left the chat session. If Persistent Chat is enabled, it requires an external database to store the chat rooms and conversations. Offline IM chat messages to be sent to users who are currently offline; these messages are stored in the local IDS database on the CUPC server.
 The Jabber XCP message routing system

The Jabber XCP message routing system has been modified in the CUPC implementation to improve functionality when users are available on multiple devices. Messages are

> Topic