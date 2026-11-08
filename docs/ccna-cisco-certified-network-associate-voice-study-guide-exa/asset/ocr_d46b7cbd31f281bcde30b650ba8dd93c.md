```
```text
Router1(config-ephone-dn)# exit
Router1(config)# exit
```
```

Now that we’ve created an ephone-dn, we can capture it into an ephone configuration by using the ephone command. This is accomplished with the following commands:

```
```text
Router1# configure terminal
Router1(config)# ephone 1
Router1(config-ephone-dn)# mac-address 00cc:00cc:00cc
Router1(config-ephone-dn)# button 1:1
Router1(config-ephone-dn)# exit
Router1(config)# exit
```
```

From the preceding command listing, you can see that the MAC address of the phone must be known. If you are using autoregistration, you can use the show ephone command to see the MAC addresses of the registered phones. Once you map an ephone to a MAC address, the settings will be saved in the router’s configuration.

The button command is used to identify the phone button that should light up when a line rings. In the preceding command example, the button 1:1 command indicates that button 1 should light up when extension 5001 (ephone 1) is called. You will also be calling from extension 5001 (ephone 1) when you press button 1 to pick up the line. The button command has more options. The first number is always the phone button, and the second number is always the ephone-dn associated with that phone button; however, the colon can be replaced with different characters. For example, the command button 1s1 would indicate a silent ring instead of a normal ring. Table 12-2 lists the options for the second space or separator character when using the button command.

| Separator Character Options for the button Command | Separator Character | Meaning |
|---|---|---|
|  | `:` | Normal ring |
|  | `b` | Call waiting beep, no ring |
|  | `c` | Overlay line (with call waiting) |
|  | `f` | Feature ring |
|  | `m` | Monitor mode |
|  | `o` | Overlay line (no call waiting) |
|  | `s` | Silent ring |
|  | `w` | Watch mode |
|  | `x` | Overlay expansion/rollover |