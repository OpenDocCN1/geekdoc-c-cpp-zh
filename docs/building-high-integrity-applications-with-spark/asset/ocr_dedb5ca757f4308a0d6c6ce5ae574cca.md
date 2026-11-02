```
```ada
function Search_For_Zero (Values : in Integer_Array) return Index_Type
with
   Pre  => (for some Index in Index_Type => Values (Index) = 0),
   Post => Values (Search_For_Zero'Result) = 0;

end Utility;
```
```

Here the assertion policy is explicitly set to Check causing the precondition (and postcondition) to be checked at runtime whenever the function is called. However, the body of this package could include

```
```ada
pragma Assertion_Policy (Ignore);
```
```

This removes all assertion checking inside the body itself. Notice, however, that all calls to Search_For_Zero will have the precondition (and postcondition) checked even if those calls come from inside the package.

The checking of the postcondition in this case is somewhat unfortunate because discharging all verification conditions in the body will have shown the postcondition is always satisfied. However, with the GNAT compiler, it is possible to use the Assertion_Policy pragma to selectively control each kind of assertion individually. See the GNAT Reference Manual (2015a) for more information. For example, the specification could be written as follows.

```
```ada
package Utility is
   pragma Assertion_Policy (Pre => Check, Post => Ignore);

   subtype Index_Type is Natural range 0 .. 1023;
   type Integer_Array is array (Index_Type) of Integer;

   function Search_For_Zero (Values : in Integer_Array) return Index_Type
   with
      Pre  => (for some Index in Index_Type => Values (Index) = 0),
      Post => Values (Search_For_Zero'Result) = 0;

end Utility;
```
```

Care is required whenever explicitly setting the assertion policy to Ignore. For example, if a change is made to the body of preceding package Utility and not all verification conditions are discharged after the change, you could easily end up with the case in which a postcondition is not satisfied and not checked. However, the SPARK tools always generate verification conditions and