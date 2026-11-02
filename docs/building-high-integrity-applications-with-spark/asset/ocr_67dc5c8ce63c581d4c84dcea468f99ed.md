```
```ada
(for all J in Items'Range =>
    (for all K in J + 1 .. Items'Last => Items(J) <= Items(K)));
end Searchers;
```
```

The precondition uses two nested for-all quantified expressions to assert that each item of the array comes before (or is the same as) all the items that follow it. The SPARK tools will, as usual, create a verification condition at each place where Binary_Search is called to prove that the precondition is satisfied.

It bears repeating that assertions in Ada are executable. With that in mind, notice that the precondition given for Binary_Search runs in $O(n^2)$ time. In contrast, the binary search algorithm itself runs in only $O(\log n)$ time.

An alternative way of expressing that the array is sorted is

```
```ada
Pre => (for all J in Items'First .. Items'Last - 1 =>
            Items (J) <= Items (J+1))
```
```

This has the advantage of running in only $O(n)$ time, and it might also be considered clearer. However, it is still asymptotically slower than the algorithm to which it is attached. Because assertions can use quantified expressions over large arrays, and even call recursive functions, they can consume large amounts of space and time. Expressive assertions thus have the potential to render unusable a program that would otherwise have acceptable performance characteristics. We discuss this issue further in Section 6.8.

# ### 6.2.2 *Postconditions*

A *postcondition* is a condition that is asserted to be true when a subprogram completes its actions and returns control to the caller. It describes the effects of the subprogram. Postconditions are, thus, formal statements derived from the functional requirements that our program must meet.

Postconditions are introduced with the Post aspect. As an example, consider the Searchers package again. A version of that package follows, where the Binary_Search procedure has been given a postcondition:

```
```ada
package Searchers2
   with SPARK_Mode => On
is
   subtype Index_Type is Positive range 1 .. 100;
   type Array_Type is array (Index_Type) of Integer;

   procedure Binary_Search (Search_Item : in  Integer;
                            Items       : in  Array_Type;
                            Found       : out Boolean;
                            Result      : out Index_Type)
```
```