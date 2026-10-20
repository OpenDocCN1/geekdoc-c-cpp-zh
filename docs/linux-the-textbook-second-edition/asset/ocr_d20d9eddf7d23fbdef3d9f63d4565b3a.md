laboratories, the Massachusetts Institute of Technology (MIT), the University of California at Berkeley, Bell Labs, and National Aeronautics and Space Administration (NASA). The number of class B addresses is relatively large, and these addresses are assigned to large commercial organizations and educational institutions. Hence, corporations such as IBM and Oracle, educational institutions such as Iowa State University, and numerous other national and international universities have been assigned class B addresses. The total number of class C addresses is quite large, so these addresses are assigned to individuals and small- to medium-sized organizations, such as local Internet service providers, small consulting and software companies, community colleges, and universities.

Although the IPv4 addressing scheme can be used to identify a large number of networks and hosts, it has not been able to cope with the rapid growth of the Internet. Among the many advantages of IPv6 is the extremely large number of hosts that can be connected. With the 128-bit address, the maximum number of hosts on the Internet will increase to roughly 2^128, which is greater than 3.4 × 10^38. This number is roughly 6 × 2^28 times the present world population. One disadvantage of IPing is that, as the address size is very large, remembering IPv6 addresses becomes very difficult. However, because most users prefer to use symbolic names, remembering IPv6 addresses should not present a problem. Also, some compact notations similar to dotted decimal notation (DDN) have been proposed for IPv6 addresses as well. Many large companies and academic institutions have been assigned IPv6 addresses, including Google, IBM, Intel, Microsoft, MIT, UC Berkeley, and Iowa State University. You can use the host command to find out if an organization has been assigned an IPv6 address, as follows:

```
$ host stanford.edu
stanford.edu has address 171.67.215.200
stanford.edu has IPv6 address 2607:f6d0:0:925a::ab43:d7c8
stanford.edu mail is handled by 10 mxa-00000d03.gs1b.pphosted.com.
stanford.edu mail is handled by 10 mxb-00000d03.gs1b.pphosted.com.
$
```

Note that IPv6 addresses are displayed in the colon-hex notation. In this notation, two hexadecimal digits are used to specify every byte of the address. A colon (:) is inserted between every two bytes—that is, four hex digits—of an address. If a number between two consecutive colons is not four digits, it represents the least significant nibbles in a two-byte sequence. For example, 82 in an address in fact is 0082, 0 is 0000, and 10 is 0010. The right most hex number for the two-byte sequence is for the least significant two bytes of the 128-bit address. Finally, two consecutive colons between the least significant hex number and previous hex number represent all zeros. The 128-bit IPv6 address of stanford.edu, consisting of 32 nibbles, is therefore represented as follows:

| MSD |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | LSD |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 2 | 6 | 0 | 7 | f | 6 | d | 0 | 0 | 0 | 0 | 9 | 2 | 5 | a | 0 | 0 | 0 | 0 | 0 | 0 | a | a | 4 | 3 | d | 7 | c | 8 |

Most Linux commands and tools have been enhanced to handle IPv6 addresses in the colon-hex notation, as follows:

```
$ host 2607:f6d0:0:925a::ab43:d7c8
8.c.7.d.3.4.b.a.0.0.0.0.0.0.0.0.a.5.2.9.0.0.0.0.0.d.6.f.7.0.6.2.ip6.arpa domain name pointer web.stanford.edu.
$
```

Here, the hex numbers are shown in the reverse order of significance—that is, least significant hex digit first. As you can see, the IPv6 address is for thumb.iastate.edu. A more detailed discussion on IPv6 addresses, including the purpose of each byte of the address, is beyond the scope of this book.

# 11.5.2.1 IPv4 Addresses in Dotted Decimal Notation

Although hosts and routers process IPv4 addresses as 32-bit binary numbers, they are difficult for people to remember. For this reason, the IPv4 addresses are given in DDN. In this notation, all four