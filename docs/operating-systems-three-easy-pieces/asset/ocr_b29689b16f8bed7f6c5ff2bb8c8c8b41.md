# DATA INTEGRITY AND PROTECTION

Another basic checksum function is addition. This approach has the advantage of being fast; computing it just requires performing 2's complement addition over each chunk of the data, ignoring overflow. It can detect changes in data, but is not good if the data, is shifted.

A slightly more complex algorithm is known as the Fletcher checksum, (as you might guess) for the inventor, John G. Fletcher [F82]. It is quite simple to compute and solves the problem of two checks, s1 and s2. Specifically, assume a block D consists of bytes d1 ... dn; s1 = (s1 + dn) mod 255 (computed over all di); s2 in turn is s2 = (s2 + s1) mod 255 (again over all di) [F84]. The Fletcher checksum is almost as strong as the CRC (see below), detecting all single-bit, double-bit errors, and many bursts [F04].

A final commonly used checksum is known as a cyclic check (CRC). Assume you wish to compute the checksum over a block D. All you do is as if it is a large number (it is a string of bytes all) and divide it by an agreed value (k). The remainder of this division is the value of the CRC. As it turns out, we can implement this by modulo operation rather efficiently, and hence the popularity of the CRC in networking as well. See elsewhere for more details [M13].

Whatever the method used, it is obvious that there is no perfect checksum: it is possible two data blocks with non-identical contents will have identical checksums, something referred to as a collision. Such thing feels intuitive: after all, computing a checksum is taking something large (e.g., 4KB) and producing a summary that is much smaller (e.g., 4 or 8 bytes). In choosing a good checksum function, we are thus trying to find one that minimizes the chance of collisions while remaining easy to compute.

# Checksum Layout

Now that you understand a bit about how to compute a checksum, let's next analyze how to use checksums in a storage system. The first question we must address is the layout of the checksum, i.e., how checksums be stored on disk?

The most basic approach stores a checksum with each disc sector (or block). Given a data block D, let us call the checksum over that data C(D). Without checksums, the disk layout looks like this:

| D0 | D1 | D2 | D3 | D4 | D5 | D6 |

With checksums, the layout adds a single checksum for every block: