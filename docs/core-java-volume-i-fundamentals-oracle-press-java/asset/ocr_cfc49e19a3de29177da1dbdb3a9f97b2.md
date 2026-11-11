# java.util.BitSet 1.0

+   - `BitSet(int initialCapacity)` constructs a bit set.

+   - `int cardinality()` 1.4 returns the number of bits that are set, or, when considered as a set of integers, the number of elements.

+   - `int length()` 1.2 returns the "logical length" (1 plus the index of the highest set bit). This is useful for iterating over the elements.

+   - `int size()` returns the number of bits currently available in the internal data structure, *not* the number of set elements.

+   - `boolean get(int bit)` gets a bit.

+   - `void set(int bit)` sets a bit.

+   - `void clear(int bit)` clears a bit.

+   - `void and(BitSet set)` logically ANDs this bit set with another.

+   - `void or(BitSet set)` logically ORs this bit set with another.

+   - `void xor(BitSet set)` logically XORs this bit set with another.

+   - `void andNot(BitSet set)` clears all bits in this bit set that are set in the other bit set.