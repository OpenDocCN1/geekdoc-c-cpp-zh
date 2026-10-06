Notice that the CRC card and UML diagram do not reflect all of the details, such as assumptions and unusual circumstances. However, after you have identified such conditions, you should specify how your methods will behave under each one. You should write down your decisions about how you want your methods to behave, as we have done in the following table. Later, you can incorporate these informal descriptions into the C++ comments that document your methods.

# ABSTRACT DATA TYPE: BAG

+   * A finite number of objects, not necessarily distinct, in no particular order, and having the same data type.
* The number of objects in this collection.

OPERATIONS

| PSEUDOCODE | DESCRIPTION |
| --- | --- |
| getCurrentSize() | Task: Reports the current number of objects in this bag.
Input: None.
Output: The number of objects currently in the bag. |
| isEmpty() | Task: Sees whether this bag is empty.
Input: None.
Output: True or false according to whether the bag is empty. |
| add(newEntry) | Task: Adds a given object to this bag.
Input: anEntry is an object.
Output: True or false according to whether the addition succeeds. |
| remove(anEntry) | Task: Removes an occurrence of a particular object from this bag, if possible.
Input: anEntry is an object.
Output: True or false according to whether the removal succeeds. |
| clear() | Task: Removes all objects from this bag.
Input: None.
Output: None. |
| getFrequencyOf(anEntry) | Task: Counts the number of times an object occurs in this bag.
Input: anEntry is an object.
Output: The integer number of times anEntry occurs in the bag. |
| contains(anEntry) | Task: Tests whether this bag contains a particular object.
Input: anEntry is an object.
Output: True or false according to whether anEntry occurs in the bag. |
| toVector() | Task: Gets all objects in this bag.
Input: None.
Output: A vector containing all entries currently in the bag. |