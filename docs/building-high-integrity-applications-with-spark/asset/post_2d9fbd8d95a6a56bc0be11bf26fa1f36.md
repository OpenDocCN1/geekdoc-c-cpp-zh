
```ada
procedure Clear;
-- # global out Contents;
-- # derives Contents from ;

end Temperature_Buffer05;
```

The abstract state of this variable package is declared in SPARK 2005 by way of "own variables" in the specification. Annotations, in the form of Ada comments, provide the data and flow dependency contracts in a largely intuitive way. Of particular interest is the precondition on procedure Get that requires Has_More to return true. It is not permitted to get an item from the buffer if it is empty.

In SPARK 2005 the use of Has_More in the precondition is abstract because SPARK 2005 annotations are not executable. Any functions used in pre- and postconditions must be pure, therefore, SPARK 2005 requires that the abstract state read by the function be passed as an explicit parameter.

The body of the package starts by refining the abstract state and declaring the constituents of that state:

```ada
package body Temperature_Buffer05
-- #own Contents is Buffer, Count, Next_In, Next_Out;
is
  Buffer_Size : constant := 8;
  type Buffer_Index_Type is mod Buffer_Size;
  type Buffer_Type is array (Buffer_Index_Type) of Temperature_Record;
  Buffer : Buffer_Type;

  type Buffer_Count_Type is range 0 .. Buffer_Size;
  Count  : Buffer_Count_Type; -- Number of items.
  Next_In : Buffer_Index_Type; -- Next available slot.
  Next_Out : Buffer_Index_Type; -- Next item to extract.
```

The use of a modular type for Buffer_Index_Type causes buffer indexes to wrap around automatically and simplifies the programming. In this case the buffer never fills; old data is pushed out as new data is entered.

The implementation of function Has_More and procedure Get follows:

```ada
function Has_More return Boolean
-- # global in Count;
is
begin
  return Count > 0;
end Has_More;

procedure Get (Item : out Temperature_Record)
--# global in Buffer; in out Count, Next_Out;
--# derives Item from Next_Out, Buffer &
--#          Count from Count           &
--#          Next_Out from Next_Out;
is
begin
   Item := Buffer (Next_Out);
   Next_Out := Next_Out + 1;
   Count := Count - 1;
end Get;
```

As with SPARK 2014, the data and flow dependencies are refined in terms of their constituents. The code itself is straightforward. However, the SPARK 2005 tools have difficulty proving that the assignment statement `Count := Count - 1` does not cause a runtime error. It does not because the precondition forbids Get from being called unless Count > 0. However, the SPARK 2005 tools do not understand the behavior of Has_More and need to be taught that behavior using techniques we do not detail here. This is necessary despite the fact that Has_More is implemented in the body of the package where, in principle, the tools can see it.

The following SPARK 2014 version of the package specification is a straightforward translation of the SPARK 2005 version:

```ada
with Data_Types;
package Temperature_Buffer14
with
   SPARK_Mode => On,
   Abstract_State => Contents
is

   type Temperature_Record is
      record
         Time_Stamp : Data_Types.Time_Type;
         Value      : Data_Types.Temperature_Type;
      end record;

-- Initializes the buffer.
procedure Clear
   with
      Global  => (Output => Contents),
      Depends => (Contents => null);

-- Adds a new item to the buffer.
```

In addition, the SPARK 2014 tools use generally more powerful theorem provers; some verification conditions that were difficult with SPARK 2005 may be easier with SPARK 2014. As a result, it may be possible to simplify or eliminate certain loop invariants or write the code in the more natural way.

Finally, the richer language provided by SPARK 2014 offers the possibility of refactoring a SPARK 2005 program to take advantage of that richness. The Temperature_Buffer example presented earlier comes from an embedded system that also buffers other kinds of readings. It would be natural to make all of the buffers instances of a single generic unit. However, earlier versions of SPARK did not support generics. Of course, how much rewriting of a legacy system is appropriate will depend on the situation. However, if it is deemed worthwhile to update the software to SPARK 2014, it may also be worthwhile to reorganize and even redesign parts of the software to take advantage of SPARK 2014’s larger set of features.

### 8.2 Legacy Ada Software

The preferred use of SPARK is in a *constructive analysis* style in which we create a program whose units contain a full set of contracts specified by the aspects discussed in Chapters 4 and 6. As we saw in Chapter 7, SPARK provides the means to mix SPARK code with non-SPARK code through the use of contracts on the specifications of non-SPARK code. Commonly, the non-SPARK code is written in Ada or C.

SPARK 2014 has the capability to analyze preexisting Ada code where no SPARK contracts are given. This *retrospective analysis* is made possible by the ability of the SPARK tools to synthesize a set of data dependency contracts and flow dependency contracts directly from the source code of a program unit (see Section 4.5). These synthesized contracts can be used to analyze legacy Ada code or during the early development of SPARK code in which contracts have not yet been included.

The synthesized contracts are safe over-approximations of the real contracts. For example, they assume that *all* outputs are dependent on *all* inputs. Because it is unlikely that the body of the subprogram meets all of the synthesized contracts, the SPARK tools do not generate warnings or checks when the body does not respect the synthesized contracts. The synthesized contracts are used to verify proper initialization and respect of any dependency contracts in the callers of the subprogram.

Section 6.8.1 of the *SPARK 2014 User’s Guide* describes how contracts are synthesized for

- a non-SPARK subprogram – one with `SPARK_Mode => Off`;
- a SPARK subprogram with no data or flow contracts;
- a SPARK subprogram with only data contracts; and
- a SPARK subprogram with only flow contracts.

As mentioned in the previous paragraph, the aspects that the SPARK tools synthesize are almost always more general than those we would write. However, when no data or flow contracts are given on a SPARK subprogram, the tools generate precise data and flow dependencies by using path-sensitive flow analysis to track data flows in the subprogram body. These synthesized contracts accurately describe the code whether or not that code is correct.

Section 7.3 of the *SPARK 2014 Toolset User’s Guide* (SPARK Team, 2014b) provides some guidance to using the SPARK tools to analyze legacy Ada code as a first step prior to performing a full or partial conversion to SPARK. Even without the intention of converting legacy Ada code to SPARK, the tools can help us find errors in our Ada code. Take, for example, the following contrived package specification and body:

```ada
package Unused_Parameter with SPARK_Mode => On is

   procedure Avg (A : in  Natural;
                  B : in  Natural;
                  C : out Natural);
end Unused_Parameter;

package body Unused_Parameter with SPARK_Mode => On is

   procedure Avg (A : in  Natural;
                  B : in  Natural;
                  C : out Natural) is
   begin
      C := (A + A) / 2;
   end Avg;

end Unused_Parameter;
```

Here we made a mistake in the body by typing (A + A) rather than (A + B). The SPARK Examine tool reports that B is not used. This analysis is not provided by the GNAT compiler. Here is another simple package:

```ada
package Overflow with SPARK_Mode => On is

   procedure Avg (A : in  Natural;
                  B : in  Natural;
                  C : out Natural);
end Overflow;

package body Overflow with SPARK_Mode => On is

   procedure Avg (A : in  Natural;
                  B : in  Natural;
                  C : out Natural) is
   begin
      C := (A + B) / 2;
   end Avg;

end Overflow;
```

This time the Examine tool reports no problems. However, the Prove tool reports that the line

```ada
C := (A + B) / 2;
```

may overflow. It is possible that the values of A and B are so large that their sum exceeds that of the largest value the accumulator can hold. This error is still present in implementations of the binary search and merge sort algorithms in many introductory programming books even after being pointed out by Pattis in 1988. While one probably would not think to test this case, our proof tool was quick to discover it. With a little algebra, we can reorganize the expression to

```ada
C := A + (B - A) / 2;
```

Now the Prove tool reports no possible runtime error.

Let us look at a larger example of using SPARK to analyze preexisting Ada code. We would like to verify that no runtime errors will be raised in the package Bingo_Basket that we presented in Section 3.4. Here is its specification with the addition of the aspect to make it in SPARK:

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
