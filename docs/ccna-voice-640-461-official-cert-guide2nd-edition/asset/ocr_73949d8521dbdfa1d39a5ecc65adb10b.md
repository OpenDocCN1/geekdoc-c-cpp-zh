**Note:** The Redundancy count shown in Table 2-4 shows the type of failover supported by the voicemail solutions. CUE and CUCM Business Edition do not support any failover. The original Cisco Unity supported Active/Passive, which meant a backup server would sit idle until the primary server failed. Cisco Unity Connection supports Active/Active, allowing the redundant servers to load balance the mailboxes.

# Cisco Unity Connection Key Features

The following are some of the notable features of Cisco Unity Connection:

+   - **Proven appliance-based platform:** Cisco Unity Connection is built on top of the same stable, hardened, appliance-based operating system as CUCM. (These two products even use the same installation DVD.)

+   - **To 20,000 mailboxes per server:** Cisco Unity Connection scales to a massive size per server. Even though Unity Connection supports a single-server configuration, most organizations will opt for a high availability pair of servers.

+   - **Access voicemails from anywhere:** Carrying on the original dream of Cisco Unity, Cisco Unity Connection allows voicemail retrieval from phone, e-mail, web browser, mobile devices, and instant-messaging platforms.

+   - **LDAP directory server integration:** Similar to CUCM, Cisco Unity Connection can integrate with an existing corporate directory (as Microsoft Active Directory) to avoid creating a duplicate database.

+   - **Microsoft Exchange support:** Cisco Unity Connection can integrate with an existing Microsoft Exchange deployment to enable fantastic features, as as different call treatment based on your Exchange calendar, e-mail text-to-speech (hear your emails from a phone), manage, manage Exchange calendar (accept, decline, cancel, and so on) from a phone, and so on.

+   - **Active/active high availability:** Cisco Unity Connection uses a Publisher/Subscriber IBM database scheme just like CUCM between a pair of servers. The pair of servers can support up to 20,000 mailboxes in a redundant fashion. Both servers can accept client requests (giving it the active/active redundancy). Typically, the largest Cisco Unity Connection server can support up to 250 voicemail ports (entries, allowing 250 people to check their voicemail at a time). By creating a high-availability pair, you can now support 500 voicemail ports.

**Note:** If one of the servers in a Unity Connection high-availability pair fails, all 20,000 mailboxes are still available, but the number of voicemail ports is reduced to the maximum supported by the single server.