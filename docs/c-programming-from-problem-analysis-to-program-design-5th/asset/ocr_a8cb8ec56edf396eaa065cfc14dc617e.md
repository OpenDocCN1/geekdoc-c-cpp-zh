Let us now generalize this problem to the case of 64 disks. To begin, the first needle contains all 64 disks. Disk number 64 cannot be moved from needle 1 to needle 3 unless the top 63 disks are on the second needle. So first, we move the top 63 disks from needle 1 to needle 2, and then we move disk number 64 from needle 1 to needle 3. Now the top 63 disks are all on needle 2. To move disk number 63 from needle 2 to needle 3, we first move the top 62 disks from needle 2 to needle 1, and then we move disk number 63 from needle 2 to needle 3. To move the remaining 62 disks, we use a similar procedure. This discussion translates into the following recursive algorithm given in pseudocode. Suppose that needle 1 contains n disks, in which n ≥ 1.

+   1. Move the top n − 1 disks from needle 1 to needle 2, using needle 3 as the intermediate needle.
+   2. Move disk number n from needle 1 to needle 3.
+   3. Move the top n − 1 disks from needle 2 to needle 3, using needle 1 as the intermediate needle.

This recursive algorithm translates into the following C++ function:

```
```cpp
void moveDisks(int count, int needle1, int needle3, int needle2)
{
    if (count > 0)
    {
        moveDisks(count - 1, needle1, needle2, needle3);

        cout << "Move disk " << count << " from " << needle1
             << " to " << needle3 << "." << endl;

        moveDisks(count - 1, needle2, needle3, needle1);
    }
}
```
```

# ## Tower of Hanoi: Analysis

Let us determine how long it would take to move all 64 disks from needle 1 to needle 3. If needle 1 contains three disks, then the number of moves required to move all three disks from needle 1 to needle 3 is 2^3 − 1 = 7. Similarly, if needle 1 contains 64 disks, then the number of moves required to move all 64 disks from needle 1 to needle 3 is 2^64 − 1. Because 2^10 = 1024 ≈ 1000 = 10^3, we have:

2^64 = 2^4 × 2^60 ≈ 2^4 × 10^18 = 1.6 × 10^19

The number of seconds in one year is approximately 3.2 × 10^7. Suppose the priests move one disk per second and they do not rest. Now:

1.6 × 10^19 = 5 × 3.2 × 10^18 = 5 × (3.2 × 10^7) × 10^11 = (3.2 × 10^7) × (5 × 10^11)

The time required to move all 64 disks from needle 1 to needle 3 is roughly 5 × 10^11 years. It is estimated that our universe is about 15 billion years old (1.5 × 10^10). Also, 5 × 10^11 = 50 × 10^10 ≈ 33 × (1.5 × 10^10). This calculation shows that our universe would last about 33 times as long as it already has.