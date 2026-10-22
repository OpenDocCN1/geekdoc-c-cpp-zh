```
template <typename E, class getKey>
void binsort(E A[], int n) {
    List<E> B[MaxKeyValue];
    E item;
    for (int i=0; i<n; i++) B[A[i]].append(getKey::key(A[i]));
    for (int i=0; i<MaxKeyValue; i++)
        for (B[i].setStart(); B[i].getValue(item); B[i].next())
            output(item);
}
```

# Figure 7.16 The extended Binsort algorithm.

Here the key value is used to determine the position for a record in the final sorted array. This is the most basic example of a Binsort, where key values are used to assign records to bins. This algorithm is extremely efficient, taking Θ(n) time regardless of the initial ordering of the keys. This is far better than the performance of any sorting algorithm that we have seen so far. The only problem is that this algorithm has limited use because it works only for a permutation of the numbers from 0 to n − 1.

We can extend this simple Binsort algorithm to be more useful. Because Binsort must perform direct computation on the key value (as opposed to just asking which of two records comes first as our previous sorting algorithms did), we will assume that the records use an integer key type. We further assume that it can be extracted from a record using the key method supplied by a template parameter class named getKey.

The simplest extension is to allow for duplicate values among the keys. This can be done by turning array slots into arbitrary-length bins by turning B into an array of linked lists. In this way, all records with key value i can be placed in bin B[i]. A second extension allows for a key range greater than n. For example, a set of n records might have keys in the range 1 to 2n. The only requirement is that each possible key value have a corresponding bin in B. The extended Binsort algorithm is shown in Figure 7.16.

This version of Binsort can sort any collection of records whose key values fall in the range from 0 to MaxKeyValue−1. The total work required is simply that needed to place each record into the appropriate bin and then take all of the records out of the bins. Thus, we need to process each record twice, for Θ(n) work.

Unfortunately, there is a crucial oversight in this analysis. Binsort must also look at each of the bins to see if it contains a record. The algorithm must process MaxKeyValue bins, regardless of how many actually hold records. If MaxKeyValue is small compared to n, then this is not a great expense. Suppose that MaxKeyValue = n². In this case, the total amount of work done will be Θ(n + n²) = Θ(n²). This results in a poor sorting algorithm, and the algorithm becomes even worse as the disparity between n and MaxKeyValue increases. In addition,