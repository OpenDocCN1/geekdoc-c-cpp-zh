# EXERCISES

10.14. Modify the simulation code from Section 10.4 to also monitor the variables service time, waiting time and total time in the system (i.e., the waiting time plus service time) for the subsets of Customer objects that have Gold values of true or false.

10.15. Rewrite the simulation example from Section 10.4 using the queue adapter with service rendered on a first-in-first-out basis according to arrival time.

10.16. Use the deque container class to modify your code from Exercise 10.15 to allow the last person in the queue to leave.

10.17. A company has a total of n machines that use to produce products; a machines are required for daily production while n machines are in reserve. The failure time for a machine has an exponential distribution with mean λ_F and the time to fail of the n machines are independent. When a machine fails, it is replaced by a reserve machine, assuming that one is available, and sent for repair. Repair times are also exponentially distributed with mean λ_R. Use the discrete event simulation technique of Section 10.5 to approximate the expected time before production comes to a halt in an active machine fails with no machines left in reserve for various values of the system parameters n, a, λ_F and λ_R.

10.18. Add a remove method to the chainClass class of Section 10.4.2.

10.19. Implement the -- operator for the iterator in the chainClass.

10.20. Add a method for resizing the example in Section 10.4.2. First, use

```
template<class Key, class Data> int
chainHash<Key, Data>::hash(Key a) {
return a % tableSize;
}
```

as the definition for the hash function in chainClass. Then, create a class/struct that has a single member of double. Equip your class/struct with the overloaded modulus operator

```
int operator%(double a, int m) {
return ((int)floor(a)) % m;
}
```

A number of other objects need to be defined before this new class/struct will work effectively with the chainHash.

10.22. Take the stock index example of Section 10.4.1 and create a database that stores the list by order of index rather than time. Write a C++ program that manages the database by inserting/adjusting it for new entries.

10.23. There are cases where it is necessary to alter a heap entry in a way that will change its priority. For example, if the heap is storing personal records by salary, and (possibly) wants to change the order of individuals in the heap. To change the priority of an item, we need to access it by name or value and the basic heap does not provide this functionality. One way to resolve this problem is to use a hash table to keep track of the elements in the heap array; that is, every object in the heap has two components: a key and a data member by which it is ordered. An object's key value is paired with its array index to create a table that tells us where to locate and, e.g., after a specific element in the heap. Use conjunction with the vector class to create a priority queue that allows for changes in the key values. Is this development necessary for the STL priority_queue class?