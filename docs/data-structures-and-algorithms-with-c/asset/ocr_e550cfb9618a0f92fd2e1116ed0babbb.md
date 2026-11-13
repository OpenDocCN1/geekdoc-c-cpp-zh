| 5 | 10 | 15 | 20 | 25 | 30 |

![](bbox=[0.592, 0.082, 0.703, 0.142])

(q)

Decrease the size of the heap by deleting last element.

| 5 | 10 | 15 | 20 | 25 | 30 |

(r)

5 is the last element of the heap, therefore the array is now sorted.

# Figure 10.15 (a-r): Heap Sort

# Algorithm of Heap Sort

```
Algorithm: HEAP_SORT (A, N)
[A is an array of N elements]
1. Repeat For I = N/2 to 1
   Call SHIFT_DOWN(A, I, N)
   End of Loop
2. Repeat For I = N TO 2
   a) Temp = A[I]
   b) A[I] = A[1]
   c) A[1] = Temp
   d) Call SHIFT_DOWN (A, 1, I-1)
   [End of Loop]
3. Return

Function: SHIFT_DOWN(A, K, N)
[A is an array of N elements, K is the position of the element that shifted down]
1. Set Parent = K, Child = 2* Parent and Temp = A[Parent]
2. Repeat while Child<=N
   a) If Child < N and A[Child + 1] > A[Child]
      then Set Child = Child + 1
   b) If Temp >= A[Child] Goto Step 3
   c) Set A[Parent] = A[Child]
   d) Set Parent = Child and Child = 2* Parent
   [End of Loop]
3. Set A[Parent] = Temp
4. Return
```

In the above algorithm, efficient shift-down version is used to build a heap by shifting operations instead of interchanging operation. When an element gradually moves downwards, it is stored in a temporary variable and if one child is greater than its children, then stores the child to its original