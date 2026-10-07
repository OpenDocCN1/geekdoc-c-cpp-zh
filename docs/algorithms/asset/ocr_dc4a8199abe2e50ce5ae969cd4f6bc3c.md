# 1.5 Universal hashing

We end this chapter with an application of number theory to the design of hashing functions. Hashing is a very useful method of storing data items in a table so as to support insertions, deletions, and lookups.

Suppose, for instance, that we need to maintain an ever-changing list of about 250 IP (Internet protocol) addresses, perhaps the addresses of the currently active customers of a Web service. Recall that an IP address consists of 32 bits encoding the location of a computer on the Internet, usually broken down into 8-bit fields, for example, 128.32.168.20). We could obtain fast lookups if we maintained the records in an array indexed by IP address. But this would be wasteful of memory: the array would have $2^{32} \approx 4 \times 10^9$ entries, the majority of them blank. Alternatively, we could use a linked list of the 250 records. But then accessing records would be very slow, taking time proportional to 250, the total number of customers. Is there a way to get the best of both worlds, to use an amount of memory that is proportional to the number of customers and yet achieve fast lookups? This is exactly hashing comes in.

# 1.5.1 Hash tables

Here's a high-level view of hashing. We will give a "nickname" to each of the $2^{32}$ possible IP addresses. You can think of this short name as a number between 1 and 250 (we will later adjust this range slightly). Many IP addresses will inevitably have the same nickname; however, most of the 250 IP addresses of our particular customers are assigned distinct names, and we will store their records in an array of size 250 indexed by these names. What if there is more than one record associated with the same name? Easy; each entry of the array points to a linked list containing all records with that name. So the total amount of storage is proportional to 250, the number of customers, and independent of the total number of possible IP addresses. Moreover, if not many customer IP addresses are assigned the same name, lookup is fast, because the average size of the linked list we have to scan is small.

But how do we assign a short name to each IP address? This is the role of a hash function: in our example, a function $h$ that maps IP addresses to positions in a table of length 250 (the expected number of data items).

![](bbox=[0.348, 0.747, 0.853, 0.903])