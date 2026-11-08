# # Part I Review Commands Mind Map Solution

+   - switchport access vlan vlan-id
+   - vlan vlan-id
+   - name vlan-name
+   - { no } shutdown
+   - { no } vlan vlan-id
+   - vtp mode { server | client | transparent }
+   - vtp { server | client }

+   - show vlan brief
+   - show vlan id vlan-id
+   - show vlan name vlan-name
+   - show vlan status
+   - switchport trunk { dynamic { auto | desirable } | trunk }
+   - switchport trunk allowed vlan { add | all | except | remove } vlan-list
+   - switchport trunk encapsulation { dot1q | isl | negotiate }
+   - switchport nonegotiate
+   - switchport mode trunk
+   - switchport trunk native vlan vlan-id

+   - show interfaces interface-id switchport
+   - show interfaces interface-id trunk

+   - vtp domain domain-name
+   - vtp password password
+   - vtp mode { server | client | transparent }
+   - vtp { version | v2 }
+   - { no } vtp pruning

+   - show vtp status
+   - show vtp password

+   - show vlan { brief }
+   - show vtp status

+   - spanning-tree mode { rapid-pvst | mst }
+   - spanning-tree { vlan vlan-number } root primary
+   - spanning-tree { vlan vlan-number } root secondary
+   - spanning-tree { vlan vlan-number } priority priority
+   - spanning-tree { vlan vlan-number } cost cost
+   - spanning-tree { vlan vlan-number } port-priority port-priority
+   - channel-group channel-group-number mode { auto | desirable | on | active | passive }
+   - spanning-tree portfast
+   - spanning-tree portfast default
+   - spanning-tree bpduguard enable
+   - spanning-tree bpdufilter enable
+   - { no } spanning-tree portfast bpduguard default
+   - { no } spanning-tree portfast default

+   - show spanning-tree
+   - show spanning-tree interface interface-id
+   - show spanning-tree { vlan vlan-id }
+   - show spanning-tree { vlan vlan-id } root
+   - show spanning-tree { vlan vlan-id } bridge
+   - show spanning-tree summary
+   - show spanning-tree interface-type interface-number portfast
+   - show etherchannel { channel-group-number } summary
+   - { clear | default } port channel-group-number

Part 1
Commands