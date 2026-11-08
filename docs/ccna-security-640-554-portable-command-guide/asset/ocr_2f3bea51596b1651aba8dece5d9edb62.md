# # ACLs in IPv6

Packet filtering in IPv6 is similar to packet filtering in IPv4. A strategy to prevent common attacks between the two protocol stacks, such as reconnaissance and spoofing attacks, typically starts with ACLs trying to match malicious traffic.

# ## Mitigating IPv6 Attacks Using ACLs

IPv6 ACLs can help mitigate the following threats, among others:

+   - Header extension threats, for instance, amplification attacks based on Routing Header (RH)
+   - Threats based on misuse and abuse of ICMPv6
+   - Reconnaissance based on multicast IPv6 addresses
+   - Threats that exploit tunneling solutions such as those used in IPv6 migration environments

**NOTE:** Some threats require a combined approach using both protocol stacks, specifically those that exploit dual-stack environments.

# ## IPv6 ACLs Implicit Entries

Each IPv6 ACL implicitly appends three lines: two permit entries to enable IPv6 neighbor discovery (ND) and the traditional rule that implements a default deny policy:

```
```
permit icmp any any nd-na
permit icmp any any nd-ns
deny ipv6 any any
```
```

**CAUTION:** It might be desirable to log all implicitly denied packets by explicitly configuring the `deny ipv6 any any log` ACE. A common mistake is to forget the two implicit ND ACEs, which result in ND issues. The solution is to explicitly add all three implicit lines, in the correct order, at the end of the ACL.

# ## Filtering with IPv6 ACLs

| Command | Description |
| --- | --- |
| `Router(config)#ipv6 access-list access-list-name` | Define an IPv6 ACL, and enter IPv6 access list configuration mode. IPv6 ACL names cannot contain a space or quotation mark or begin with a numeral. |