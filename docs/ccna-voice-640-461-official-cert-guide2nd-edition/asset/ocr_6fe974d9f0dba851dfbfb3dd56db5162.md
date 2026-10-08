# Example 6-1 Identifying Voice Ports Using voice port summary

| CME_Voice# show voice port summary |
| PORT | CH | SIG-TYPE | ADMIN OPER STATUS | STATUS | EC |
|---|---|---|---|---|---||
| 0/0/0 | | fxs-1ls | up | dorm on-hook | idle | y |
| 0/0/1 | | fxs-1ls | up | dorm on-hook | idle | y |
| 0/2/0 | | fxo-1ls | up | dorm idle | on-hook | y |
| 0/2/1 | | fxo-1ls | up | dorm idle | on-hook | y |
| 0/2/2 | | fxo-1ls | up | dorm idle | on-hook | y |
| 0/2/3 | | fxo-1ls | up | dorm idle | on-hook | y |

**Note:** If you are using your router for Cisco Unified Communication Manager Express (CME), each phone-dn you configure shows up under the **show voice port summary** output as an EXFS port.

Based on the output from Example 6-1, you can see that this router is equipped with two FXS ports and four FXO ports.

FXS ports have three common areas of configuration:

+   - Signaling
- Call progress tones
- Caller ID information

You can use two types of signaling for analog FXS interfaces: The signal type dictates the method used by the attached device to signal that a phone is going off-hook. Table 6-2 briefly describes the differences between ground start and loop start signaling.

# Table 6-2 Comparing Ground Start and Loop Start

| Ground Start | Loop Start |
|---|---|n| Signals a new connection by grounding two of the wires in the cable temporarily | Signals by completing a circuit (by lifting the handset off-hook) and dropping the total DC voltage down the line |
| Must be configured | Is the default |
| Typically used when connecting to PBX equipment | Typically used when connecting to analog devices, such as telephones, fax machines, and | |

You can use the syntax shown in Example 6-2 to set the signaling type on the voice port.