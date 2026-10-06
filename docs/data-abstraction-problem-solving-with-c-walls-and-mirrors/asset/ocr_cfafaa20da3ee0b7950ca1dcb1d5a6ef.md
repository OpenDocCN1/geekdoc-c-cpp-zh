# Hashing 549

Now consider a more efficient way to compute 474,757. Rather than converting the previous binary number to decimal, you can evaluate the expression

$14 	imes 32^3 + 15 	imes 32^2 + 20 	imes 32^1 + 5 	imes 32^0$

This computation is possible because we have represented each character as a 5-bit binary number, and $2^i$ is 32.

By factoring this expression, you can minimize the number of arithmetic operations. This tech-nique is called Horner’s rule and results in

```
$((14 \times 32 + 15) \times 32 + 20) \times 32 + 5$$
```

Although both these expressions have the same value, the result in either case could very well be larger than a typical computer can represent; that is, an overflow can occur. If you use the hash function

```
$h(x) + x \pmod m$
```

you can prevent an overflow by applying the modulo operator after each parenthesized expression in Horner’s rule. The implementation of this algorithm is left as an exercise.

> **Programming Tip:** You can use the following function getHashIndex—in your programs. C++ Inheritance 7 will discuss the Standard Template Library (STL) and make use of the way that this function uses.
```cpp
template <class KeyType, class ItemType>
int HashDictionary<KeyType, ItemType>::
getHashIndex(const KeyType& key) const {
    // We create a hash function type called HashFunction that hashes
    // a search key. First we create an unordered_map object for our KeyType
    // and itype.
    std::unordered_map<KeyType, ItemType> mapper;

    // We invoke the method function to return the hash function
    // for the KeyType and assign it to #hashFunction
    typename std::unordered_map<KeyType, ItemType>::type hashFunction = mapper.hash_function();

    // Need static_cast because hashFunction returns an unsigned integer
    return static_cast<int>(hashFunction(key) % hashTableSize);
}
// getHashIndex
```

# 18.4 Resolving Collisions

Consider the problems caused by a collision. Suppose you want to insert an item into whose hash table, the key is 4567 into the hash table, as described previously. The hash function $h(x) = x \pmod{101}$ tells you to place the new item in table[22], because 4567 mod 101 is 22. Suppose, however table[22] already contains an item, Figure 18-10. Earlier if you had placed 7597 into table[22] because 7597 mod 101 equals 22, where do you place the new item? You do not want to discard the insertion on the grounds that the dictionary is full: You could have a collision even when inserting into a dictionary that contains only one item!