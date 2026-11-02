```
```ada
package body Overflow with SPARK_Mode => On is

   procedure Avg (A : in  Natural;
                  B : in  Natural;
                  C : out Natural) is
   begin
      C := (A + B) / 2;
   end Avg;

end Overflow;
```
```

This time the Examine tool reports no problems. However, the Prove tool reports that the line

```
```ada
C := (A + B) / 2;
```
```

may overflow. It is possible that the values of A and B are so large that their sum exceeds that of the largest value the accumulator can hold. This error is still present in implementations of the binary search and merge sort algorithms in many introductory programming books even after being pointed out by Pattis in 1988. While one probably would not think to test this case, our proof tool was quick to discover it. With a little algebra, we can reorganize the expression to

```
```ada
C := A + (B - A) / 2;
```
```

Now the Prove tool reports no possible runtime error.

Let us look at a larger example of using SPARK to analyze preexisting Ada code. We would like to verify that no runtime errors will be raised in the package Bingo_Basket that we presented in Section 3.4. Here is its specification with the addition of the aspect to make it in SPARK:

```
```ada
with Bingo_Numbers; use Bingo_Numbers;
package Bingo_Basket with SPARK_Mode => On is

   function Empty return Boolean;

   procedure Load  -- Load all the Bingo numbers into the basket
     with
        Post => not Empty;

   procedure Draw (Letter  : out Bingo_Letter;
                   Number : out Callable_Number)
```
```