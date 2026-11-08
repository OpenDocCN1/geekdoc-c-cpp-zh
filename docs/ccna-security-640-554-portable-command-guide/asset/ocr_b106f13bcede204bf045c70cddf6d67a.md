![](bbox=[0.089, 0.088, 0.822, 0.538])

The mirror configuration should only be used as a guide when configuring the peer. The following configuration MUST NOT be directly applied to the peer device.

```
```text
crypto isakmp policy 2
 authentication pre-share
 encr aes 128
 hash sha
 group 5
 lifetime 86400
 exit
crypto isakmp policy 1
 authentication pre-share
 encr 3des
 hash sha
 group 2
 lifetime 86400
 exit
crypto isakmp key cisco123 address 209.165.200.225
crypto ipsec transform-set R1-R3-Transform-Set
 esp-sha-hmac esp-aes 128
 mode tunnel
 exit
ip access-list extended SDM_1
 remark CCF-ACL Category=4
 remark IPSEC Rule
 permit ip 192.168.0.0 0.0.0.255 192.168.1.0 0.0.0.255
 exit
crypto map SDM_MAP 1 ipsec-isakmp
 description Apply the crypto map on the peer router's interface
  having IP address 209.165.200.129 that connects to this router.
 set transform-set R1-R3-Transform-Set
 set peer 209.165.200.225
 match address SDM_1
 exit
```
```

**Figure 17-14**  Generated Text File in Notepad

> **NOTE:** The mirror configuration does not apply the crypto map to the peer interface. Therefore, the `crypto map <crypto-map-name>` command must be configured on the peer VPN interface.

Finally, copy and paste the edited configuration to the remote peer global configuration. The VPN tunnel should now be tested.

# Testing and Monitoring IPsec VPNs

Navigate to Configure > Security > VPN > Site-to-Site VPN > Edit Site-to-Site VPN to open the VPN screen shown in Figure 17-14.

Click the Test Tunnel button, and then click Start. CCP generates interesting traffic and enables the VPN tunnel. CCP displays status messages indicating the results of the test, as shown in Figure 17-15.