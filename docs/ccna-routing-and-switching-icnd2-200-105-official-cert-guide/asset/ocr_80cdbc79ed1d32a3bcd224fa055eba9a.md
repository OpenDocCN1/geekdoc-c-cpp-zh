DTP can also negotiate whether the two devices on the link agree to trunk at all, as guided by the local switch port's administrative mode. The administrative mode refers to the configuration setting for whether trunking should be used. Each interface also has an *operational* mode, which refers to what is currently happening on the interface, and might have been chosen by DTP's negotiation with the other device. Cisco switches use the **switchport mode** interface subcommand to define the administrative trunking mode, as listed in Table 1-2.

# **Table 1-2**   Trunking Administrative Mode Options with the **switchport mode** Command

| Command Option | Description |
| :--- | :--- |
| access | Always act as an access (nontrunk) port |
| trunk | Always act as a trunk port |
| dynamic desirable | Initiates negotiation messages and responds to negotiation messages to dynamically choose whether to start using trunking |
| dynamic auto | Passively waits to receive trunk negotiation messages, at which point the switch will respond and negotiate whether to use trunking |