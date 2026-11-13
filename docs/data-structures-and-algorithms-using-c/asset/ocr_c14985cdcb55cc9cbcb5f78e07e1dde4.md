![](bbox=[0.146, 0.053, 0.853, 0.396])

So now, we are in a position to design an algorithm for Tower of Hanoi with more than two disks. We divide the stack of disks in two parts. The largest disk (n<sup>th</sup> disk) is in one part and all other (n-1) disks are in the second part.

Our ultimate aim is to move disk **n** from source to destination and then put all other (n1) disks onto it. We can imagine to apply the same in a recursive way for all given set of disks.

The steps to follow are –

**Step 1** – Move n-1 disks from **source** to **aux** **Step 2** – Move n<sup>th</sup> disk from **source** to **dest** **Step 3** – Move n-1 disks from **aux** to **dest**

A recursive algorithm for Tower of Hanoi can be driven as follows –

```
START
Procedure Hanoi(disk, source, dest, aux)
IF disk == 0, THEN
move disk from source to dest
ELSE
Hanoi(disk - 1, source, aux, dest) // Step 1 move disk from source to dest // Step 2
Hanoi(disk - 1, aux, dest, source) // Step 3
END IF
END Procedure STOP
```

To check the implementation in C programming, click here.