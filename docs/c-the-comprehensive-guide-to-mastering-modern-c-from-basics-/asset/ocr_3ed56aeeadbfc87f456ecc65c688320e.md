requires reading and writing back the neighboring values as well, which costs time.

A bitset stores each value in its own memory cell. If you want to change a single value, it can be written directly. However, this data structure requires (at least) eight times the space.

In C++, good performance can mean low memory usage on the one hand and time consumption on the other—or both. Regarding memory, there is a clear statement: `vector<bool>` saves space. And speed? That is harder to answer and depends on the system. Is it faster if you don't have to consider the neighbors, or is memory plus cache so slow that using eight times memory is also slower?

If it is important for your problem, measure and compare! I can give you a reference point. On an Intel i7-4xxx, a single experiment showed that the wasteful bitset is about twice as fast as the space-saving `vector<bool>`—and up to five times as fast as the naive implementation with `bool[]`.