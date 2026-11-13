
*definition of the load factor, $\alpha$*

$\alpha = \frac{\text{Number of occupied table locations}}{\text{The size of the table's array}}$

For open-address hashing, each array element holds at most one item, so the load factor can never exceed 1. But with chaining, each array position can hold many items, and the load factor might be higher than 1.

## **Average search time for open addressing (linear probing).**

Open-address hash tables with linear probing have just one hash function. Collisions are resolved by stepping forward, probing consecutive array elements. With linear probing, and no deletions, Knuth's formula for the average time of a successful search is as follows:

> **Searching with Linear Probing**
> 
> In open-address hashing with linear probing, a nonfull hash table, and no deletions, the average number of table elements examined in a successful search is approximately
> 
> \(\frac{1}{2} \left( 1 + \frac{1}{1-\alpha} \right)\)

This formula is not exact, but it is a good approximation when the load factor ($\alpha$) is below 1. You might notice that the formula completely fails when $\alpha$ is 1, since there is then a division by zero. But that situation would indicate a full hash table, and you should avoid getting close to full anyway. If you insist on a full hash table of $n$ elements, Knuth shows that the average time for a successful search is approximately $\sqrt{n/(\pi/8)}$ —but better yet, steer clear of full tables, and you can use the preceding formula. In addition, for a nonfull table, the formula's derivation also assumes that we have not deleted any items, and that the hash function does a good job of uniformly distributing all possible keys throughout the array (which is called **uniform hashing**).

As an example of how to use the formula, suppose that we plan to put 649 entries in a table with a capacity of 811. This provides a load factor of 649/811, or about 80%. On average, we expect successful searches to examine three table elements, as shown here:

\(\frac{1}{2} \left( 1 + \frac{1}{1-\alpha} \right) = \frac{1}{2} \left( 1 + \frac{1}{1-0.8} \right) = 3.0\)

## **Average search time for open addressing (double hashing).**

You have seen that open-address hash tables with double hashing provide some relief from clustering. The result is a smaller average time, given by the following formula (which uses "ln" to denote the natural logarithm of a number):

### Searching with Double Hashing

In open-address hashing with double hashing, a nonfull hash table, and no deletions, the average number of table elements examined in a successful search is approximately:

$$ \frac{-\ln(1-\alpha)}{\alpha} $$

As with the previous formula, this estimate is approximate. It depends on a non-full hash table, no deletions, and using a hash function with uniform hashing.

You don't need to memorize the formula, but you should know how to use it along with the ln key on your calculator. For example, ln(0.2) is about -1.6, so with a load factor of 0.8 we expect to examine an average of two elements in a successful search, as shown here:

$$ \frac{-\ln(1-\alpha)}{\alpha} = \frac{-\ln(0.2)}{0.8} = \frac{1.6}{0.8} = 2 $$

This is an improvement over the linear probing with the same load factor.

### Average search time for chained hashing.

With chaining, each element of the table's array is a head pointer for a linked list, and each of these linked lists may have several items. Therefore, the load factor may be higher than one in this formula:

### Searching with Chained Hashing

In chained hashing, the average number of table elements examined in a successful search is approximately:

$$ 1 + \frac{\alpha}{2} $$

Once again, this estimate is approximate, and it depends on using uniform hashing. Unlike the other two formulas, the chaining formula remains valid even with deletions.

With a load factor of 0.8, chained hashing expects to examine only 1.4 items during a successful search. Some other possible load factors are shown in Figure 12.8, where you can compare the average numbers for the three different hashing methods.

## FIGURE 12.8 Average Number of Table Elements Examined During a Successful Search

| Load factor (α) | Open addressing with linear probing 1/2 (1 + 1/(1-α)) | Open addressing with double hashing -ln(1-α)/α | Chained hashing 1 + α/2 |
|---|---|---|---|
| 0.5 | 1.50 | 1.39 | 1.25 |
| 0.6 | 1.75 | 1.53 | 1.30 |
| 0.7 | 2.17 | 1.72 | 1.35 |
| 0.8 | 3.00 | 2.01 | 1.40 |
| 0.9 | 5.50 | 2.56 | 1.45 |
| 1.0 | | | 1.50 |
| 2.0 | Not applicable | | 2.00 |
| 4.0 | | | 3.00 |

## Self-Test Exercises for Section 12.4

- 25. Suppose that you place 180 items in a hash table with an array size of 200. What is the load factor? For each of the three hash methods, what is the average number of table elements that you expect to have examined during a successful search?

- 26. You want to place 1000 elements in a hash table, and you'd like an average search to examine just two table elements. How big does the table's array need to be? Give separate answers for the three hash methods.

## 12.5 PROGRAMMING PROJECT: A TABLE CLASS WITH STL VECTORS

### A New Table Class

We have discussed table classes implemented with an array of records (for open-address hashing) and an array of linked lists (for chained hashing). A table class can also be implemented with existing STL containers. This is advantageous in that the table can easily access and modify data items using the member functions of the containers. We suggest the STL vector class to implement a new version of the table class. The STL vector class is analogous to a dynamic array for which certain member functions automatically increase the size of the array. It uses subscripting to access elements (such as v[2] = 10 for a vector v of integer values). Appendix H provides details for using the vector template class. Like the table in Figure 12.7 on page 616, this table will use chained hashing, but there are a few changes in the design.

### Using Vectors in the New Table

In the original version, the table was an array called data. Each location data[i] was the head pointer for a linked list of all the records with a hash value of i. The new version will use vectors instead of linked lists:

> **The New Table Is an Array of Vectors**
> Each data[i] will be a vector that contains all the records
> with a hash value of i.

### Template Parameters That Are Constants

Until now, all our template parameters have been data types, such as the RecordType for our table. However, a template parameter can also be a constant value that is used throughout the class definition. This will change our template prefix as shown here:

```
template <class RecordType, size_t TABLE_SIZE>
class table
{
    // In this definition, we'll use RecordType and the constant TABLE_SIZE.
    ...
```

> **Template Parameters Can Be Constant Values**
> A template parameter can be a constant value, and that
> constant can then be used throughout the template's definition.
> Our new table will have a template parameter for the
> TABLE_SIZE constant.

### Template Parameters That Are Functions

We no longer require RecordType to have an explicit key member variable. This gives us more flexibility in the kinds of records that can be stored. However, we will need a new mechanism to compute the key of a record. This will be done by a function with the following prototype:

```
int hashkey(const RecordType& r);
```

When we need to compute a key for a record r, the function will use hashkey(r).

But how does the new table class obtain the hashkey function? The programmer who writes the table class can't write hashkey because the RecordType is unknown. The answer is that hashkey can be provided as a third template parameter for the table class, like this:
