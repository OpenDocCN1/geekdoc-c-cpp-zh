The procedure compacts Buffer by removing occurrences of Erase_Character. Free space opened at the end of the buffer is filled with instances of Fill_Character. On returning, the value of Valid is a count of the number of original characters that were not erased.

6.10 Let the specification of the Buffers package on page 203 be modified to use an unconstrained array type as follows:

```
package Buffers_Unconstrained is
  subtype Buffer_Count.Type is Natural;
  subtype Buffer_Index.Type is Positive;
  type Buffer_Type is array(Buffer_Index.Type range <>) of Character;
  ...
end Buffers_Unconstrained;
```

Repeat Exercise 6.9.

6.11 Loop variant pragmas are not needed for many loops in SPARK programs. Under what circumstances is it appropriate to consider using a loop variant?

6.12 When a loop variant pragma is used with multiple expressions, it is possible that later expressions might “go the wrong way” as long as an earlier expression changes in the right direction. In particular, a later expression might get reset to some initial value. Explain why the loop must still eventually terminate despite this behavior. How does this relate to nested loops?

6.13 The precondition of Binary_Search does not actually need to state that the input array is sorted. A weaker, but still adequate, precondition is that the array must be partitioned by both the expressions E < Search_Item and E <= Search_Item, where E is an array element. An array is partitioned by an expression if there exists an index i such that the expression is true for every element before i and false for every element at or above i. For example, if the search item is 10, the array containing (5, 3, 10, 10, 8, 6) is suitably partitioned.

Modify the precondition on Binary_Search shown on page 167 to use this weaker condition. Does the implementation given on page 214 still satisfy the postcondition?

6.14 Consider the In_Unit_Square function on page 185. Following the style of that function, show the specification of an In_Unit_Circle function taking Float parameters and that returns +1 if the given point is in a circle with radius one centered on the origin.

6.15 The generic package Double_List discussed in Section 6.7 is incomplete. Make the package usable by adding subprograms for iterator movement