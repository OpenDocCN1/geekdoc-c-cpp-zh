The following list details a good process to find VTP configuration problems, organized into a list for easier study and reference.

+   1. **Step 1.** Confirm the switch names, topology (including which interfaces connect which switches), and switch VTP modes.
+   2. **Step 2.** Identify sets of two neighboring switches that should be either VTP clients or servers whose VLAN databases differ with the `show vlan` command.
+   3. **Step 3.** On each pair of two neighboring switches whose databases differ, verify the following:
+      - **A.** Because VTP messages only flow over trunks, at least one operational trunk should exist between the two switches (use the `show interfaces trunk`, `show interfaces switchport`, or `show cdp neighbors` *command*).
+      - **B.** The switches must have the same (case-sensitive) VTP domain name (`show vtp status`).
+      - **C.** If configured, the switches must have the same (case-sensitive) VTP password (`show vtp password`).
+      - **D.** The MD5 digest should be the same, as evidence that both the domain name and any configured passwords are the same on both switches (`show vtp status`).
+      - **E.** While VTP pruning should be enabled or disabled on all servers in the same domain, having two servers configured with opposite pruning settings does not prevent the synchronization process.
+   4. **Step 4.** For each pair of switches identified in Step 3, solve the problem by either troubleshooting the trunking problem or reconfiguring a switch to correctly match the domain name or password.