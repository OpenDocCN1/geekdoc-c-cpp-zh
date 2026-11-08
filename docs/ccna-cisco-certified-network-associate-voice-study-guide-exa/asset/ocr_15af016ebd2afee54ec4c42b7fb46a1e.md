> > **Exam Watch**
> >
> > Make sure you remember these protocols and the role they play in an H.323 network. Specifically, remember that UDP carries voice data and TCP is used for call setup. UDP is also used for call reporting and signaling (H.225 RAS messages).

In addition to these protocols, the H.323 VoIP network will use several different device types. These devices are covered in the following section.

# ## H.323 Devices

Several devices may be used on an H.323 network. The H.323 standard suggests four primary devices:

+   - Terminals
+   - Gateways
+   - Gatekeepers
+   - Multipoint Control Units (MCUs)

# ### Terminals

Terminals are the devices or software applications that communicate with each other using the H.323 protocols. A terminal can be a unique device, such as a Cisco IP phone, or it can be a desktop or laptop computer running a software-based H.323 terminal, such as a Cisco SoftPhone. H.323 terminals must support a minimum set of requirements to qualify as a standards-based terminal. These requirements are

+   - H.245 support for terminal capability or feature exchange and the creation of media communication channels
+   - H.225 support for call signaling and call setup
+   - H.225 RAS support for registration, admission control, and bandwidth management when a gatekeeper is present