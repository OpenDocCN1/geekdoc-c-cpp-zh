that at least seven characters are output. To address this, we change the loop invariant to

```
**pragma** Loop_Invariant (Count >= 2*(J-1) and Count <= 4*(J-1));
```

Now the tools are able to discharge all verification conditions in the subprogram, proving that it is free of any possibility of runtime error.

It might seem as if this process would have been easier if the types had not been so precisely defined. For example, if Address_Length_Type had a lower bound of one instead of seven, perhaps the final step would not have been necessary. However, loosening type definitions for the sake of making certain proofs easier is almost never the right approach. In fact, loosely specified types typically make proofs more difficult, if not in one place then in another. The tools might be able to use the tight constraint on Address_Length_Type to its advantage when proving verification conditions elsewhere related to IP addresses. Always strive to tighten type definitions; avoid loosening them. Embed as much information as you can into the program.

This example also illustrates the interplay between human reasoning and the SPARK tools. After convincing ourselves of the correctness of the code, we could have just, perhaps, recorded our reasoning in a comment and not bothered with finding suitable SPARK assertions. However, SPARK serves to check our work, which is valuable because humans are very error prone when trying to mentally manage the mass of details required while reasoning about programs. Also, the SPARK assertions are a form of machine readable documentation that can be checked automatically by other programmers less familiar with the code. If a change is made to the procedure, the SPARK tools will alert the programmer making the change to any potential runtime issues introduced.

As an example, consider the following code from the To_IPv4_String procedure:

```
-- Compute the digit characters for this octet.
Value   := Address (J);
Digit_2 := Digit_Lookup_Table (Value / 100);
Value   := Value rem 100;
Digit_1 := Digit_Lookup_Table (Value / 10);
Value   := Value rem 10;
Digit_0 := Digit_Lookup_Table (Value);
```

It is necessary that the values used to index the lookup table are all in the range 0 .. 9. No doubt the programmer considered that when writing the code initially. The SPARK tools also proved this without comment so the programmer did not need to spend time reviewing the code for that error. The tools can thus take care of many “simple” proofs and only require human assistance for the