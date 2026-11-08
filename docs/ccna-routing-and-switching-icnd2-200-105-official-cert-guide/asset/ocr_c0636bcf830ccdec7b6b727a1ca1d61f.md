Of course, there are key differences between IPv4 and IPv6 ACLs as well. IPv4 ACLs match IPv4 packets only (and not IPv6), and match special fields found only in IPv4 headers. Likewise, IPv6 ACLs match against IPv6 address fields as well as other fields unique to an IPv6 header. The following is a summary of the key differences:

+   - IPv4 ACLs can only match IPv4 packets and IPv6 ACLs can only match IPv6 packets.
+   - IPv4 ACLs can be identified by number or name, while IPv6 ACLs use names only.
+   - IPv4 ACLs identify that an ACL is either standard or extended based on the ACL number range or by using the standard or extended keyword. IPv6 ACLs have a similar standard and extended ACL concept, but do not differentiate the styles with a different configuration keyword.
+   - IPv4 ACLs can match on specific values unique to an IPv4 header (e.g., option, precedence, ToS TTL, fragments).
+   - IPv6 ACLs can match on specific values unique to an IPv6 header (e.g., flow label, DSCP) as well as extension and option header values.
+   - IPv6 ACLs have some implicit **permit** statements at the end of each ACL, just before the implicit deny all at the end of the ACL, while IPv4 ACLs do not have implicit **permit** statements.