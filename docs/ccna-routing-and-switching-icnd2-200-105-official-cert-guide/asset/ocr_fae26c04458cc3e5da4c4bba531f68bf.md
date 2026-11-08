| Command | Description |
|---|---|
| no frame-relay lmi-type | Interface configuration mode command that reverts back to the default LMI setting of autosensing the LMI type |
| bandwidth *num* | Interface subcommand that sets the router’s perceived interface speed |
| frame-relay map [*protocol* *protocol-address* *dlci*] [broadcast] [ietf \| cisco] | Interface configuration mode command that statically defines a mapping between a network layer address and a DLCI |
| frame-relay interface-dlci *dlci* [ietf \| cisco] | Subinterface configuration mode command that links or correlates a DLCI to the subinterface |
| keepalive *sec* | Interface configuration mode command that defines whether and how often LMI status inquiry messages are sent and expected |
| interface serial *number.sub* [point-to-point \| point-to-multipoint] | Global configuration mode command that creates a subinterface or references a previously created subinterface |
| [no] frame-relay inverse-arp | Physical and multipoint subcommand to disable Frame Relay Inverse ARP (no inverse-arp) or enable it |

**Table I-5 — Appendix I IEXC Command Reference**

| Command | Description |
|---|---|
| show frame-relay pvc [interface *interface*\|*dlci*] | Lists information about the PVC status |
| show frame-relay lmi [*type number*] | Lists LMI status information |
| show frame-relay map [*type number*] | Lists Frame Relay mapping information matching next-hop IP addresses to local DLCIs |
| show interfaces [*type number*] | Lists statistics and details of interface configuration, including the encapsulation type |
| show ip interface brief | Lists one line of output per interface with IP address and interface status |
| debug frame-relay lmi | Displays the contents of LMI messages |