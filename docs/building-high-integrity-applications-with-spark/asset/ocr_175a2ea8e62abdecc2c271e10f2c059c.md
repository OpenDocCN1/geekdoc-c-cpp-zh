A common approach to determining whether two arrays are permutations is to sort each array and compare the sorted arrays. As we are using the permutation property to verify our sort procedure, we cannot use the sort to verify the permutation. Another approach is to count the number of each element in each array and compare the counts. As our array components are integers, this approach could require 2³² counters for 32-bit integer representations.

We take another approach to show that the result is a permutation of the original. Function Perm is a ghost function. The aspect Import states that the body of the function is external to the Spark program. Rather than write a body, we will give the proof tool the mathematical rules it needs to verify our permutation postcondition. Here is the complete package body that implements our selection sort:

```
pragma Spark_Mode (On);
package body Sorters is

function Perm_Transitive (A, B, C : Array_Type) return Boolean
  with Global => null,
    Post => (if Perm_Transitive' Result
        and then Perm (A, B)
        and then Perm (B, C)
        then Perm (A, C)),
    Ghost => True,
    Import => True;

procedure Swap (Values : in out Array_Type;
    X : in Positive ;
    Y : in Positive )
  with Depends => (Values => (Values, X, Y)),
    Pre => (X in Values'Range and then
        Y in Values'Range and then
        X /= Y),
    Post => Perm (Values'Old, Values)  and then
        (Values (X) = Values'Old (Y) and then
        Values (Y) = Values'Old (X) and then
        (for all J in Values'Range =>
        (if J /= X and J /= Y then Values (J) = Values'Old (J))))
is
  Values_Old : constant Array_Type := Values
    with Ghost => True;
  Temp : Integer;
```