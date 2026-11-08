To take advantage of the ability to delete and insert lines in an ACL, both numbered and named ACLs must use the same overall configuration style and commands used for named ACLs. The only difference in syntax is whether a name or number is used. Example 17-6 shows the configuration of a standard numbered IP ACL, using this alternative configuration style. The example shows the power of the ACL sequence number for editing. In this example, the following occurs:

+   1. **Step 1.** Numbered ACL 24 is configured using this new-style configuration, with three permit commands.
+   2. **Step 2.** The `show ip access-lists` command shows the three permit commands with sequence numbers 10, 20, and 30.
+   3. **Step 3.** The engineer deletes only the second permit command using the **no 20** ACL subcommand, which simply refers to sequence number 20.
+   4. **Step 4.** The `show ip access-lists` command confirms that the ACL now has only two lines (sequence numbers 10 and 30).
+   5. **Step 5.** The engineer adds a new deny command to the beginning of the ACL, using the **5 deny 10.1.1.1** ACL subcommand.
+   6. **Step 6.** The `show ip access-lists` command again confirms the changes, this time listing three commands, sequence numbers 5, 10, and 30.

> **NOTE** For this example, note that the user does not leave configuration mode, instead using the `do` command to tell IOS to issue the `show ip access-lists` EXEC command from configuration mode.

# **Example 17-6 — _Editing ACLs Using Sequence Numbers_**

```
```text
! Step 1: The 3-line Standard Numbered IP ACL is configured.
R1# configure terminal
Enter configuration commands, one per line.  End with Ctrl-Z.
R1(config)# ip access-list standard 24
R1(config-std-nacl)# permit 10.1.1.0 0.0.0.255
R1(config-std-nacl)# permit 10.1.2.0 0.0.0.255
R1(config-std-nacl)# permit 10.1.3.0 0.0.0.255

! Step 2: Displaying the ACL's contents, without leaving configuration mode.
R1(config-std-nacl)# do show ip access-lists 24
Standard IP access list 24
    10 permit 10.1.1.0, wildcard bits 0.0.0.255
    20 permit 10.1.2.0, wildcard bits 0.0.0.255
    30 permit 10.1.3.0, wildcard bits 0.0.0.255

! Step 3: Still in ACL 24 configuration mode, the line with sequence number 20 is deleted.
R1(config-std-nacl)# no 20

! Step 4: Displaying the ACL's contents again, without leaving configuration mode.
```
```