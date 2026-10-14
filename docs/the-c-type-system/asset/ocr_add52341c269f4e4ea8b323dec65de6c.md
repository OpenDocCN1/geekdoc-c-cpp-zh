# The ValueType.GetHashCode Method

As Chapter 5 explained, the elements in a HashSet are unique; every key in the table exists only once. A new object is added to a HashSet only if it doesn't already exist in the table; otherwise, it's ignored.

When we add an item to the HashSet in this example, the implementation uses GetHashCode to identify existing keys with the same hash code. The fact that the hash codes are the same doesn't necessarily mean any of the existing keys have the same value as the new item. If no existing key has the same hash code as the new item, the new object is added to the table. If one or more existing keys have hash codes that match the new item's hash code, the Equals method is used to determine whether the item should be added. Each key with the same hash code is compared with the new item in turn, and if no match is found, the new item is added to the table as a new key.

Having Equals being called so often in our test indicates that GetHashCode for our Color type is producing hash codes that aren't well distributed. When the first element is added to the hash table, Equals isn't called at all, because there's nothing to compare with. If the second element has an identical hash code to the first, Equals is called to determine if they're identical keys. This process will repeat for each subsequent element that has the same hash code as an existing key.

If all of the Color objects in the initial sequence of 25,000 elements produce identical hash codes but have different values, adding the final new element will require a call to Equals for all of the existing 24,999 keys.

In fact, the default implementation of ValueType.GetHashCode inherited by the Color struct will likely produce many identical hash codes, regardless of whether the Color instances have different values. The reason is related to the poor performance of the implementation of Equals provided by ValueType, and it explains why the number of calls to Equals is so close to the triangular number of the sequence length.

If instances of a struct can be compared using the fast bitwise comparison for Equals, the ValueType.GetHashCode method produces hash codes based on the bit pattern of the instance in memory. If, on the other hand, the struct isn't eligible for the fast bitwise comparison, the default GetHashCode implementation considers only the first non-null instance field of the struct—the Red property in our Color type—with the result that we can get a maximum of only 256 unique hash codes. We solve that problem by implementing our own GetHashCode method to produce more unique hash codes, preferably so that each distinct Color value produces a unique hash code.

# The HashCode.Combine Method

In Listing 8-6, we add our own override of GetHashCode for the Color struct to complement our overridden Equals method, and implement the new GetHashCode by using the HashCode.Combine method from the Standard Library.