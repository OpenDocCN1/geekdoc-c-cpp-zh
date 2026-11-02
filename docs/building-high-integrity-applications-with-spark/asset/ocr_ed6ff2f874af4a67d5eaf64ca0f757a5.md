the subprograms to which they are attached. We noted this effect, for example, when discussing the Binary_Search example in Section 6.2.1. Consequently, assertions have the potential to slow down programs by a huge factor, making them thousands or even millions of times slower in some cases. For programs that rely on highly efficient algorithms, removing unnecessary assertions could make the difference between meeting performance goals and total unusability.

For this reason some compilers, such as GNAT, do not execute assertions by default. Instead they are only executed by explicitly setting the assertion policy to Check. This can be done for all assertions in the program using a compiler command line option or by setting the configuration pragma Assertion_Policy to the desired policy. Once the Spark tools have proved that all assertions will never fail, you can disable them by explicitly setting the policy to Ignore, or in the case of GNAT, simply fall back to the default behavior. It is of course necessary to recompile the program if you change the assertion policy for the change to take effect.

Of particular interest are assertions that you might wish to ignore inside a package body but still enforce at the interface to the package. Suppose, for example, that you have successfully discharged all verification conditions in a certain package body. That means, among other things, that the preconditions on internal subprograms are satisfied at every call site in that body. If you compile the body with the assertion policy set to Ignore, you will remove the overhead associated with those precondition checks. However, you might still want to have preconditions on the public subprograms checked, at least until you have shown that every call site in the entire program necessarily satisfies them. To do this, you can set the assertion policy on the specification where the public subprograms are declared to Check.

The rule is that the assertion policy used for a particular assertion is that which is in force at the point the assertion is defined. Thus, even though the compiler inserts pre- and postcondition checks into the body of the subprograms to which they apply, it is the assertion policy in effect in the specification that affects the pre- and postconditions of public subprograms.

For example, consider the function Search_For_Zero discussed on page 157. A utility package containing this function might have a specification, in part, as follows:

```
```ada
package Utility is
   pragma Assertion_Policy (Check);

   subtype Index_Type is Natural range 0 .. 1023;
   type Integer_Array is array (Index_Type) of Integer;
```
```