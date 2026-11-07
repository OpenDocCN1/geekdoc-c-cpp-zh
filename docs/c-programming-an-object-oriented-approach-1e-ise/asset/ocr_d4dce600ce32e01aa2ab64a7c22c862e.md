# Program 16.29  Merge sort process applied to two files (Continued)

```
```cpp
36    strm1 >> first;
37    strm2 >> second;
38    while (strm1 || strm2)
39    {
40        if (first <= second)
41        {
42            strm3 << first << " ";
43            strm1 >> first;
44            if (!strm1)
45            {
46                first = sentinel;
47            }
48        }
49        else
50        {
51            strm3 << second << " ";
52            strm2 >> second;
53            if (!strm2)
54            {
55                second = sentinel;
56            }
57        }
58    }
59    // Closing files
60    strm1.close();
61    strm2.close();
62    strm3.close();
63    return 0;
64 }
```
```

# 16.6.2  Symmetric Ciphers

Transmission of information using files must be handled in a secure way. One of the common techniques used for this purpose is cryptography. **Cryptography**, a word with Greek origins, means “secret writing.” It involves two distinct mechanisms: symmetric-key and asymmetric-key cryptography. Cryptography uses keys to change an original message, called *plaintext*, to a secret message, called *ciphertext*.

There are two broad categories of cryptography: *symmetric* and *asymmetric*. We discuss and use an example of the first in this section; we use an example of the second in the next section.

In *symmetric-key cryptography* we use the same key for both encryption and decryption. The key can be used for bidirectional communication, which is why it is called *symmetric*. Figure 16.16 shows the general idea behind a symmetric-key cipher.

In Figure 16.16, an entity, Alice, sends a message to another entity, Bob, over an insecure channel with the assumption that an adversary cannot understand the contents of the message by simply eavesdropping over the channel.