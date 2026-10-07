# DATA INTEGRITY PROTECTION

| C(0) | D0 | C(1) | D1 | C(2) | D2 | C(3) | D3 | C(4) | D4 |

Because checksums are usually small (e.g., 8 bytes), and disks can only be written in sector-sized chunks (512 bytes) or multiples thereof, one problem arises that is to avoid the above layout. One solution employed by drive manufacturers is to format the drive with 520-byte sectors; an extra 8 bytes per sector can be used to store the checksum. In disks that don't have such functionality, the file system must figure out a way to store the checksums packed into 512-byte blocks. One such possibility is as follows:

| C(0) | D0 | C(1) | D1 | C(2) | D2 | C(3) | D3 | C(4) | D4 |

In this scheme, the $n$ checksums are stored together in a sector, followed by $n$ data blocks, followed by another checksum sector for the next $n$ blocks, and so forth. This approach has the benefit of working on all disks, but can be less efficient; if the file system, wants, to overwrite block $D1$, it has to read the checksum sector containing $C(D1)$, update $C(D1)$ in it, and then write out the checksum sector and new data block $D1$ (thus, one read and two writes). The earlier approach (of one checksum sector) just performs a single write.

# 45.4 Using Checksums

With a layout decided out, we can now proceed to understand how to use the checksums. When reading a block $D$ the client (e.g., file system or storage controller) also reads its checksum from disk $C(D)$, which we call the *stored checksum* (hence the subscript $C_s$). The client then computes the checksum over the retrieved block $D$, which we call the *computed checksum* $C_c$. At this point, the client compares the stored and computed checksum: if they are equal (i.e., $C_c(D) = C_s(D)$), the data has not been corrupted, and can be safely returned to the user. If they do not match (i.e., $C_c(D) \neq C_s(D)$), this implies the data has changed since the time it was stored (since the stored checksum reflects the value of that data at time). In this case, we have a corruption, which our checksum has helped to detect.

Given a corruption, the natural question is what we should do about it? If the storage system has a redundant copy, the answer is: try to use it instead. If the storage system has no such copy, the answer is

© 2008–19, ARPAC-DUSSEAU

THREE
EASY
PIECES