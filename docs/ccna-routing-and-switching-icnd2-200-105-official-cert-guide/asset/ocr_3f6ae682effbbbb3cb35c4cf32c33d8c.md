+   - Line 1: Match and permit all packets with a source address of exactly 10.1.1.1.
+   - Line 2: Match and deny all packets with source addresses with first three octets 10.1.1.
+   - Line 3: Match and permit all addresses with first single octet 10.

Figure 16-7 shows the updated version of Figure 16-4, but with the completed, correct
syntax, including the WC masks. In particular, the note of use of WC mask 0.0.0.255 in the
second command, telling R2 to ignore the last octet of the number 10.1.1.0, and the WC
mask 0.255.255.255 in the third command, telling R2 to ignore the last three octets in the
value 10.0.0.0.

![](bbox=[0.149, 0.31, 0.8, 0.481])

**Figure 16-7** *Syntactically Correct ACL Replaces Pseudocode from Figure 16-4*

Finally, note that when using a WC mask, the access-list command’s loosely defined *source*
parameter should be a 0 in any octets where the WC mask is a 255. IOS will specify a source
address to be 0 for the parts that will be ignored, even if nonzero values were configured.

# ### Binary Wildcard Masks

Wildcard masks, as dotted-decimal (DDN) values, actually represent a 32-bit binary
number. As a 32-bit number, the WC mask actually directs the router’s logic bit by bit. In
short, a WC mask bit of 0 means the comparison should be done as normal, but a binary 1
means that the bit is a wildcard, and can be ignored when comparing the numbers.

Thankfully, for the purposes of CCENT and CCNA R&S study, and for most real-world
applications, you can ignore the binary WC mask. Why? Well, we generally want to match
a range of addresses that can be easily identified by a subnet number and mask, whether it
be a real subnet, or a summary route that groups subnets together. If you can describe the
range of addresses with a subnet number and mask, you can find the numbers to use in your
ACL with some simple decimal math, as discussed next.

> **NOTE**  If you really want to know the binary mask logic, take the two DDN numbers
> the ACL will compare (one from the access-list command, and the other from the packet
> header) and convert both to binary. Then, also convert the WC mask to binary. Compare
> the first two binary numbers bit by bit, but also ignore any bits for which the WC mask
> happens to list a binary 1, because that tells you to ignore the bit. If all the bits you checked
> are equal, it’s a match!