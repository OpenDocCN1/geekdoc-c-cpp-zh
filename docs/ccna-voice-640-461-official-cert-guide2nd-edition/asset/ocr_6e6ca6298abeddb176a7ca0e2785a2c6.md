# Chapter 7. Configuring Cisco CME Voice Productivity Features 191

![](bbox=[0.095, 0.063, 0.805, 0.465])

Figure 7-13 Advanced Call Park Features Available from CCP

![](bbox=[0.095, 0.525, 0.805, 0.692])

Figure 7-14 Designing Call Pickup Groups

The configuration of call pickup is incredibly simple: Just design your groups of phones and assign the ephone-dns to the groups. Example 7-7 assigns ephone-dns 1, 2, and 3 to the SALES group and ephone-dns 4, 5, and to the ACCOUNTING group, as shown in Figure 7-14.

# Example 7-7 Configuring Call Pickup

```
CME_Voice(config)# ephone-dns 1
CME_Voice(config-ephone-dn)# pickup-group 5509
CME_Voice(config-ephone-dn)# ephone-dns 2
CME_Voice(config-ephone-dn)# pickup-group 5509
CME_Voice(config-ephone-dn)# ephone-dns 3
```