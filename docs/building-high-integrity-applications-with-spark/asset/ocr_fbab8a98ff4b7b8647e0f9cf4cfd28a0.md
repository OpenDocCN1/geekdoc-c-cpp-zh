```
```ada
type Very_Long (Length : Digit_Index_Type) is
   record
      Long_Digits : Digits_Array_Type (0 .. Length - 1); -- illegal
   end record;
```
```

Unfortunately, this is illegal in Ada because the value of the discriminant cannot be used as part of an expression inside the record.

The body of package Very_Longs is too long to display fully here but may be found on http://www.cambridge.org/us/academic/subjects/computer-science/programming-languages-and-applied-logic/building-high-integrity-applications-spark. However, it is instructive to look at Number_Of_Digits. That function is too complicated to easily implement as an expression function. Instead it must be implemented as an ordinary function in the package body as the following shows:

```
```ada
function Number_Of_Digits (Number : in Very_Long) return Digit_Count_Type
with
   Refined_Post =>
      (Number_Of_Digits'Result <= Number.Length) and
      (if Number_Of_Digits'Result > 0 then
         Number.Long_Digits (Number_Of_Digits'Result) /= 0) and
      (for all J in (Number_Of_Digits'Result + 1) .. Number.Long_Digits'Last
         => Number.Long_Digits (J) = 0)
is
   Digit_Count : Digit_Count_Type := 0;
begin
   if not Is_Zero (Number) then
      for Index in Number.Long_Digits'Range loop
         if Number.Long_Digits (Index) /= 0 then
            Digit_Count := Index;
         end if;

         pragma Loop_Invariant
           ((if Digit_Count > 0 then
                (Number.Long_Digits (Digit_Count) /= 0 and
                 Digit_Count in 1 .. Index)) and
            (if Index > Digit_Count then
                (for all J in Digit_Count + 1 .. Index =>
                    Number.Long_Digits (J) = 0)));
      end loop;
   end if;
   return Digit_Count;
end Number_Of_Digits;
```
```

For SPARK to have any hope of proving the body of Divide free of runtime error, it will need to know how Number_Of_Digits works in terms of the full view