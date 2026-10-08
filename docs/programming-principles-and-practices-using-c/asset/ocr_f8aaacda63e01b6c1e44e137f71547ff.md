An **ostream** converts typed objects to a stream of characters (bytes):

![](bbox=[0.24, 0.13, 0.87, 0.34])

An **istream** converts a stream of characters (bytes) to typed objects:

![](bbox=[0.24, 0.39, 0.86, 0.61])

An **iostream** is a stream that can act as both an **istream** and an **ostream**. The buffers in the diagrams are “stream buffers” (**streambufs**). Look them up in an expert-level textbook if you ever need to define a mapping from an **iostream** to a new kind of device, file, or memory.

There are three standard streams:

**Standard I/O streams**

| | |
|----|----|
| **cout** | the standard character output (often by default a screen) |
| **cin** | the standard character input (often by default a keyboard) |
| **cerr** | the standard character error output (unbuffered) |