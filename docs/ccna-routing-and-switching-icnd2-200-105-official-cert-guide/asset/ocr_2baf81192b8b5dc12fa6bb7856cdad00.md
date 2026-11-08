To ensure that each access interface has been assigned to the correct VLAN, engineers simply need to determine which switch interfaces are access interfaces instead of trunk interfaces, determine the assigned access VLANs on each interface, and compare the information to the documentation. The show commands listed in Table 4-1 can be particularly helpful in this process.

**Table 4-1  Commands That Can Find Access Ports and VLANs**

| EXEC Command | Description |
|---|---|
| `show vlan brief`<br>`show vlan` | Lists each VLAN and all interfaces assigned to that VLAN (but does not include operational trunks) |
| `show vlan id *num*` | Lists both access and trunk ports in the VLAN |
| `show interfaces *type number* switchport | Identifies the interface’s access VLAN and voice VLAN, plus the configured and operational mode (access or trunk) |
| `show mac address-table` | Lists MAC table entries, including the associated VLAN |