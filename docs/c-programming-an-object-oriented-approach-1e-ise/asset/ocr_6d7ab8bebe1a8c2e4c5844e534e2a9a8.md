# **Program 17.10** Towers of Hanoi (Continued)

```
```cpp
41 {
42   cout << "Move top disk from " << start << " to " << end << endl;
43 }
```
```

```
```text
Run:
Enter number of disks (1 to 4): 1
Move top disk from A to C

Run:
Enter number of disks (1 to 4): 2
Move top disk from A to B
Move top disk from A to C
Move top disk from B to C

Run:
Enter number of disks (1 to 4): 3
Move top disk from A to C
Move top disk from A to B
Move top disk from C to B
Move top disk from A to C
Move top disk from B to A
Move top disk from B to C
Move top disk from A to C
```
```

The first run is trivial; we have one disk, which we move from A to C. The second run is simple; we move the top disk from A to B (auxiliary), we move the second disk to the destination, and we move the first disk from B to C. The third run takes seven moves. The first three steps move the top two disks from A to B (auxiliary). The fourth step moves the last disk from A to C. The last three steps move the two disks from B to C (using A as an auxiliary). Figure 17.16 shows the original and seven steps to move three disks.

![](bbox=[0.31, 0.607, 0.8, 0.878])

Figure 17.16   Steps to move three disks