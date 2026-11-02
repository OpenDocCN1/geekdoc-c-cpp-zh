Ada's full coverage rules require that every possible value of N be accounted for in the various when clauses. In this example that is not the case since because there are natural numbers that are neither even nor prime. However, the compiler cannot be expected to know this without understanding the detailed semantics of the predicates used to define the subtypes. Those predicates might involve calling functions of significant complexity, such as is the case for Prime_Type in this example. Thus, the example is ruled out because it uses subtypes defined with dynamic predicates.

Ada defines a more restricted form of subtype predicate, called a static predicate, that does support many (although not all) of the usual features of subtypes while still allowing some degree of customization. Furthermore, at the time of this writing, SPARK supports static predicates.

The precise rules for the kinds of predicate specifications that can be used as static predicates is given in section 3.2.4 of the Ada Reference Manual (2012). However, as one example, we show a static predicate using a membership test to specify a non-contiguous range of values. Consider a package for managing a game of Scrabble. The specification of the package might be, in part, shown as follows:

```
```ada
pragma SPARK_Mode(On);
package Scrabble is

   subtype Scrabble_Letter is Character range 'A' .. 'Z';

   subtype Scrabble_Value is Positive
     with Static_Predicate => Scrabble_Value in 1 .. 5 | 8 | 10;

   type Scrabble_Word is array(Positive range <>) of Scrabble_Letter;

   subtype Scrabble_Score is Natural range 0 .. 100;
   function Raw_Score (Word : in Scrabble_Word) return Scrabble_Score
     with Pre => (Word'Length <= 10);

end Scrabble;
```
```

Here a subtype Scrabble_Letter is used to constrain Character to just the uppercase letters used by the game. The subtype Scrabble_Value is defined with a static predicate to only contain the values that are actually used on the various letters. The type Scrabble_Word is an unconstrained array of letters intended to hold a single word. The function Raw_Score adds together the value of the letters in the given word and returns it as a value in the range from 0 to 100. The