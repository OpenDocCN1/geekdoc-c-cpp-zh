The next parameter in the command configures this group of users to use one of three SNMPv3 *security levels*. As you can see from the summary in Table 26-2, all three security levels provide message integrity for their messages, which confirms that the message has not been changed in transit. The **auth** option adds authentication to message integrity, using a username and password, with IOS storing the password with a hash and never sending the password as clear text. The last increase in security level, configured by using the **priv** security level, causes the SNMP manager and agent to encrypt the entire SNMP packet for all SNMP messages sent, in addition to performing message integrity and authentication.

**Table 26-2 — SNMPv3 Security Levels Keywords and Their Meanings**

| Command Keyword | Keyword in Messages | Checks Message Integrity? | Performs Authentication? | Encrypts Messages? |
|---|---|---|---|---|
| noauth | noAuthNoPriv | Yes | No | No |
| auth | authNoPriv | Yes | Yes | No |
| priv | priv | Yes | Yes | Yes |