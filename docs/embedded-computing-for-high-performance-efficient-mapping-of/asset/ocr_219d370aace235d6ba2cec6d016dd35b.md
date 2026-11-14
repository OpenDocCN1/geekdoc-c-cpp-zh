the new flattened loop and to limit the execution of the blocks at the level of the outermost loop according to the original loop definition. Also, loop flattening is always a legal loop transformation since the original execution order is not modified.

```
LOOP Outer
Body_1;
LOOP Inner
Body_2;
End Inner;
End Outer;

Loop Flatten: FlatIndex = Outer x max(Inner)
If(Last iteration of Inner (FlatIndex))
Body_1;
Body_2;
If(Last iteration of Inner (FlatIndex))
Body_3;
End FlatLoop
```

# 5.6.4 LOOP FUSION AND LOOP FISSION

Loop fusion (also known as loop merge) and loop fission (also known as loop distribution) merge a sequence of loops into one loop and split one loop into a sequence of loops, respectively.

Unlike other loop transformations previously mentioned, these two loop transformations change the order in which operations are executed, and therefore are only legal if the original data dependencies are preserved. With respect to data dependencies, loop fusion is legal if it does not introduce antidependences. Flow dependences are supported if they exist between the original loops before performing loop fusion. If the trip count of the loops being merged is not the same, the fusion of the loops needs additional code to enable the execution of the original iteration space for each loop’s block of code. With respect to data dependences, loop fission is illegal when there are lexically backward loop-carried data dependences.

Despite these restrictions, both transformations present various potential benefits (see, e.g., [4]). Loop fusion may increase the level of parallelism, data locality, and decrease the loop control overhead (by reducing the number of loops), but may also increase the pressure on register allocation. Loop fission, on the other hand, might be used to distribute computations and memory accesses in a way that may increase the potential for loop pipelining and loop vectorization, may reduce cache misses, and may decrease the pressure on register allocation. There are also cases where loop fusion allows the use of scalar replacement to array variables (also known as array contraction, as data may not need to be fully stored and can be communicated using scalars. Conversely, the use of loop fission may require that some scalars be stored in arrays (known as scalar expansion) to be available to other loops). Loop fission can also enable other transformations such as loop interchange.

# 5.6.5 LOOP INTERCHANGE AND LOOP PERMUTATION (LOOP REORDERING)

Loop interchange (also known as iteration interleaving) changes the order of execution between two loops in a loop nest (see, e.g., [5]). The technique is useful to improve the data memory access patterns and thus increase the overall code spatial locality. Also, it can enable other important code transformations. Loop permutation