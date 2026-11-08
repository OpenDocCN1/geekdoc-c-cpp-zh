| Container | Description |
|---|---|
| `vector<bool>` | Specialized container; stores bool compactly |
| `array<bool,n>` | Regular container; stores bool values separately |
| `bitset<n>` | Compact, but not a standard container; rather like a large unsigned with bit operations |

Table 24.12  Profile: The bool containers.

# 24.11.1  Dynamic and Compact: “vector<bool>”

One might assume that a vector<bool> wastes a lot of space: a bool is normally as large as an int for performance reasons, even though a single bit would suffice to store true or false.

In the case of vector<bool>, the standard library has a specialization where bits are compacted. Multiple true/false values share a memory space. This means that a container vector<bool>(100) takes up much less memory than bool[100].

Externally, vector<bool> behaves like a normal sequence container for bool—with one exception: the access methods cannot provide a bool& for in-place modification. A reference into the vector would always hit multiple bits at once. Instead of a bool&, you get back a proxy object that “pretends” to be a bool& and takes on the task of actually writing into the vector<bool> when it matters.

Do not use vector<bool> without protection against concurrent writes in parallel operation: the proxy object cannot handle it.

# 24.11.2  Static: “array<bool,n>” and “bitset<n>”

If you think that array<bool,n> is also specialized for compactness, you are mistaken. Unlike vector<bool>, array<bool> is not optimized for compactness; there is no specialization for it in the standard library. This means that an array<bool,100> takes up as much memory as bool[100].

If you need a fixed-size array of bool, you are better off using bitset<>. Although it is not a real container, it is compact and has the added advantage that you can perform bit operations directly, such as bitwise AND (&)—almost as if they were the bits in an unsigned or similar. If it is the interface of a container that you need, such as iterators, then use a vector<bool>. An example with some—but not all—operations is shown in Listing 24.90.