```
```ada
-- Draw a random number from the basket
   with
      Pre => not Empty;

end Bingo_Basket;
```
```

When we run the SPARK Examine tool we see the following messages concerning the package body (code on page 84):

```
```text
Phase 1 of 2: generation of Global contracts...
Phase 2 of 2: analysis of data and information flow...
bingo_basket.adb:34:07: warning: no Global contract available for "Reset"
bingo_basket.adb:34:07: warning: assuming "Reset" has no effect on global items
bingo_basket.adb:36:26: warning: no Global contract available for "Random"
bingo_basket.adb:36:26: warning: assuming "Random" has no effect on global items
```
```

It is obvious that the Examine tool is not happy with our use of the generic random value generator from the Ada library. Our solution here is to factor out the code involving operations from the library and put it into a private child package. We mark the specification as in SPARK and the body as not in SPARK:

```
```ada
private package Bingo_Basket.Random with SPARK_Mode => On is
   function Random_Number return Callable_Number;
end Bingo_Basket.Random;
```
```

```
```ada
with Ada.Numerics.Discrete_Random;
package body Bingo_Basket.Random with SPARK_Mode => Off is

   package Random_Bingo is new Ada.Numerics.Discrete_Random
                   (Result_Subtype => Callable_Number);

   -- The following object holds the state of a random Bingo number generator
   Bingo_Gen : Random_Bingo.Generator;

   function Random_Number return Callable_Number is
   begin
      return Random_Bingo.Random (Gen => Bingo_Gen);
   end Random_Number;

begin
   -- Initialize the random number generator from the system clock
   Random_Bingo.Reset (Gen => Bingo_Gen);
end Bingo_Basket.Random;
```
```