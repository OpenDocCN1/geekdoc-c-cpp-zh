inside a value with a fixed number of bits without overflow. These are the kinds of integers we show in our example. The full specification of package Very_Longs with line numbers for reference is as follows:

```
```ada
1   pragma SPARK_Mode(On);
2
3   package Very_Longs is
4
5   --- Here "Digit" means a base 256 digit.
6   Maximum_Length : constant := 2**16;
7   type    Digit_Count_Type is new Natural range 0 .. Maximum_Length;
8   subtype Digit_Index_Type is Digit_Count_Type range 1 .. Digit_Count_Type'Last;
9   type    Very_Long (Length : Digit_Index_Type) is private;
10
11  --- Constructors.
12  function Make_From_Natural (Number : in Natural;
13                              Length : in Digit_Index_Type) return Very_Long
14    with Post => Make_From_Natural'Result.Length = Length;
15
16  procedure Make_From_Hex_String (Number : in String;
17                                  Result : out Very_Long;
18                                  Valid  : out Boolean)
19    with
20      Depends => ((Result, Valid) => (Number, Result)),
21      Pre => Number'Length = 2*Result.Length;
22
23  --- Relational operators. Only Very_Longs of equal size can be compared.
24  function "<" (L, R : in Very_Long) return Boolean
25    with Pre => L.Length = R.Length;
26
27  function "<=" (L, R : in Very_Long) return Boolean
28    with Pre => L.Length = R.Length;
29
30  function ">" (L, R : in Very_Long) return Boolean
31    with Pre => L.Length = R.Length;
32
33  function ">=" (L, R : in Very_Long) return Boolean
34    with Pre => L.Length = R.Length;
35
36  --- Returns True if Number is zero.
37  function Is_Zero (Number : in Very_Long) return Boolean;
38
39  --- Returns the number of significant digits in Number.
```
```