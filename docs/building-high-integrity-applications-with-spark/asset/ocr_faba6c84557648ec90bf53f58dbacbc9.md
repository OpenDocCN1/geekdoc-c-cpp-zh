```
```
   Swap (Values => Values,
          X      => Current,
          Y      => Smallest);
   end if;

   pragma Assume (Perm_Transitive (Values'Loop_Entry, Values'Last, Values));

   pragma Loop_Invariant (Perm (Values'Loop_Entry, Values));
   pragma Loop_Invariant  -- Simple partition property
     ((for all J in Current .. Values'Last =>
          Values (Current) <= Values (J)));
   pragma Loop_Invariant  -- order property
     ((for all J in Values'First .. Current =>
          Values (J) <= Values (J + 1)));
   end loop;
   end Selection_Sort;
end Sorters;
```
```

The heart of the permutation verification is in procedure Swap starting on line 14. Its postcondition states that (1) the resulting array is a permutation of the original array; (2) the values at index locations X and Y were swapped; and (3) the rest of the values in the array are unchanged.

We know that swapping two elements in an array creates a permutation of the original array. However, the SPARK tools do not know this fact. We use pragma Assume on line 34 with the ghost function Perm to state this fact. After swapping two elements, the SPARK tools will assume that the result is a permutation of the original. We used the ghost constant Values.Old to hold a copy of the original array. We could not use Values'Old as the 'Old attribute can only be used in postconditions.²

Next we have to tell the SPARK tools that after multiple element swaps the final array is a permutation of the original array. This is a transitivity property: if A and B are permutations and B and C are permutations, then A and C are permutations. We use another ghost function, Perm.Transitive defined on lines 4–11, to express this transitivity. The postcondition of this function states the transitivity property. A function postcondition should always mention the result of the function so we have also included it. As the postcondition is all we need for our proof, we included the aspect Import so we do not have to write a body for this function.

The pragma Assume on line 78 tells the proof tools that after each swap, the result is still a permutation of the original. The three parameters of the call to Perm.Transitive in this pragma are the original array (its value prior to the start of