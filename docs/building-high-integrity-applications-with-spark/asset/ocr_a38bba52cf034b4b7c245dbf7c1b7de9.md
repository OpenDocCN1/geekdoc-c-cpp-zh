when the subtraction overflows the range of Integer. If the code proves free of runtime error, neither of these cases can occur; the program cannot have both an infinite loop and a satisfied loop variant at the same time.

Unfortunately, the implementation of Binary_Search in Section 6.4 does contain a possible infinite loop, and as you would expect, the loop variant fails to prove. To fix the subprogram, it is necessary to correct the error in such a way as to maintain the proofs of freedom from runtime error, the post-condition, and some suitable loop variant. An implementation that does so follows:

```
```ada
package body Searchers3
   with SPARK_Mode => On
is
   procedure Binary_Search (Search_Item : in Integer;
                            Items       : in Array_Type;
                            Found       : out Boolean;
                            Result      : out Index_Type) is
      Low_Index  : Index_Type := Items'First;
      Mid_Index  : Index_Type;
      High_Index : Index_Type := Items'Last;
   begin
      Found  := False;
      Result := Items'First;   -- Initialize Result to "not found" case.

      -- If the item is out of range, it is not found.
      if Search_Item < Items(Low_Index) or Items(High_Index) < Search_Item then
         return;
      end if;

      loop
         Mid_Index := (Low_Index + High_Index) / 2;
         if Search_Item = Items(Mid_Index) then
            Found  := True;
            Result := Mid_Index;
            return;
         end if;

         exit when Low_Index = High_Index;

         pragma Loop_Invariant (not Found);
         pragma Loop_Invariant (Mid_Index in Low_Index .. High_Index - 1);
         pragma Loop_Invariant (Items(Low_Index) <= Search_Item);
```
```