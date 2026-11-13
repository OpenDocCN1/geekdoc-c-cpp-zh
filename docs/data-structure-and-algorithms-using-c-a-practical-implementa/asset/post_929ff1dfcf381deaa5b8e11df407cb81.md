
```
finish = clock(); //time in milliseconds
    duration = (double) ( (finish-start)); //time in secs.
    timetaken[3][5] = duration;
    delete a;
    //assign 50000 to n
    n = 50000;
    input(n);
start = clock(); //time in milliseconds
insertion(n);
finish = clock(); //time in milliseconds
    duration = (double) ( (finish-start)); //time in secs.
    timetaken[4][5] = duration;
    delete a;
```

```
//print the details
cout<<endl<<"SELECTION HEAP QUICK MERGE BUBBLE INSERTION\n\n";
for(i=0;i<5;i++)
{
cout<<(i+1)*10000<<"\t";
for(j=0;j<6;j++)
{
cout<<timetaken[i][j]<<"\t";
}
cout<<endl;
}
```

# OUTPUT

| | SELECTION | HEAP | QUICK | MERGE | BUBBLE | INSERTION |
|---|---|---|---|---|---|---|
| 10000 | 292 | 2 | 2 | 2 | 337 | 88 |
| 20000 | 1232 | 3 | 8 | 4 | 1455 | 361 |
| 30000 | 2150 | 6 | 8 | 6 | 3107 | 791 |
| 40000 | 3655 | 7 | 10 | 8 | 5557 | 1406 |
| 50000 | 5510 | 9 | 14 | 10 | 5184 | 2194 |

Process exited after 33.76 seconds with return value 0
Press any key to continue ...

## 10.10 Questions

- 1. With detailed steps, sort 12,34,54,6,78,34,2,33,41,87 using heap sort.
- 2. Write the algorithm for Quick sort.
- 3. Write a program to implement the merge sort.
- 4. Write a single program to compare selection sort, insertion sort, and bubble sort by generating 1000 random numbers.
- 5. Compare all sorting techniques in terms of time taken by them to sort 10,000 randomly generated numbers.
- 6. When are binary search and linear search implemented? Explain with an example.
- 7. Sort 123,435,678,8765,32,23,4,56 using radix sort.

A Hash table is simply an array that is addressed via a function. For Ex. The below hash table is an array with eight elements. Each element is a pointer to a linked list of numeric data. The hash function for this example is simply divides the data key by 8, and uses the remainder as an index into the table. This yields a number from 0 to 7. Since the Range of indices for hash Table is 0 to 7. To insert a new item in the table, we hash the key to determine which list the term goes on and then insert the item at the beginning of the list. Ex to insert 11, we divide 11 by 8 whose remainder is 3. Thus, 11 goes on the list starting at hash table [3]. To find a number we hash the number and chain down the correct list to see if it is in the table. To delete a number we find the number and remove and remove the node from the linked list.

## 11.1 Hash Functions

The hash functions are chosen to avoid collision and also with simple operations. When we choose a particular hashing method is noted that hash function should not be biased towards any particular slot in the hash table so as to minimize collision. Also a hash function will have the characteristic that each key is likely to hash to anyone of the slots available in the hash table. Some of the hash functions are

### Division Method

This method is considered as a simplest method. In this method integer x is divided by M and then by using the remainder. This method is also called as the division method of hashing.

The format of hash function will be H(x) = x mod m;
This method works fine for just about any value of M. While choosing the value of M some care should be taken and it is better to take an large prime number. A way making M as a large prime number the keys are spread out evenly. The advantage of the division hash function is simplicity and drawback of this method is due to the property that conjunctive keys are mapped consecutive hash values.

### Middle Square Method

The middle square method employs hashing method that avoids the use of division and the working of this hash method is that a key is multiplied by itself and the address is obtained by choosing an appropriate number of bits or digits from the middle of the square. The selection depends upon the table size and also they should fit into one computer word of memory. The same positions in the square must be used for all keys.

Ex: 56,789 squaring it the number becomes 3,224,990,521. If three digit address is needed then choose 990.

### Multiplication Method

We can form this hashing method by making slight variation in middle-square method. In this technique instead of multiplying the value by itself we have to multiply the number by a constant and then extract the middle K bits from the result.

### Folding Method

In this technique a key is divided into a number of parts and each part should have equal length. The exception should given to the last part. The splitted parts are then added together and if we get final carry it should be ignored.

Ex : Let us consider 456,123,789. Now this key is divided into three subparts and adding them we will get 456 + 123 + 789 = 1386.

So by ignoring the final carry of 1 we will have 368 and this method is called as fold-shifting.

A slight variation can also be implemented by reversing the first and last subparts. This process is known as foldboundary method.

## 11.2 Collisions

It is not guarantee that the hash function will generate the unique hash key value for all the entries. It also happened that two or more entries having a same key value. So in that situation these two records have to place at the same hash table and also in the same position, which does not possible. This situation leads to the collision. So it is work to find out a space for the newly allocated element. The problem of avoiding these collisions is the challenge in designing a good hash function.A good hash function minimizes collisions by spreading the elements uniformly throughout the array. But Minimization of the collision is very difficult.

## 11.3 Collision Resolution Methods

### Linear Probing

A simple approach to resolving collisions is to store the colliding record into the next available space. This technique is known as linear probing. Linear probing resolves hash collision by sequential searching a hash table beginning at the location returned by the hash function. What happens if the key hashes to the last index in the array and that space is in use? We consider the array as circular structure and continue looking for an empty room at the beginning of the array.

Ex: Consider a hash function as h(x) = x%7 Then arrange the numbers 23,50,30,38 in the hash table

| 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|
| | 50 | 23 | 30 | 38 | | |

### Quadratic Probing

In this case, when collision occurs at the hash address h, then this method searches the table at location h+1, h+4, h+9, etc. The hash function is defined as (h(x) + i²) % hash size.

Ex : The numbers are 23,81,93,113 The function is h(x) = x % 10

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|
| | 81 | | 23 | 93 | | | 113 | | |

### Separate chaining

The hash function is h(x) = x %10

Store the numbers 23,45,56,78,81,38,113

![](img/1faaa0256577c74e8a61f42967760aa8_397_0.png)

Entries in the hash table are dynamically allocated and entered on a linked list associated with each hash table entry. This technique is known as Chaining. An alternative method, where all entries are stored in the hash table itself, is known as direct or open addressing and may be found in the references.

## 11.4 Clustering

One problem with the linear probing is that its results in a situation called clustering. A good hash function results in a uniform distribution of indexes throughout the array, each room equally likely to be filled.

### Bucket and Chaining

Another alternative way for handling Collisions is to allow multiple element keys to hash to the same location. One solution is to let each computed hash location contain rooms for multiple elements rather than just a single element. Each of these multi-element locations is called buckets. Using this approach, we can allow collisions to produce duplicate entries at the same hash location, up to a point. When the becomes full we must again deal with handling collisions.

Another solution, which avoids this problem, is to use the hash value not as the actual location of the element, but as the index into an array of pointers. Each pointer accesses a chain of elements that share the same hash location.
