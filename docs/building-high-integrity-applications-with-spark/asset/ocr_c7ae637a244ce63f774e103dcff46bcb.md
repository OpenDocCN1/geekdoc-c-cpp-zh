```
```ada
Volt_IO.Put (Item => V,
             Fore => 1,
             Aft  => 2,
             Exp  => 0);
   Put_Line (" volts ");
end Ohms_Law;
```
```

This program also illustrates the *use type clause*. When we declare a type, we define its domain and a set of operations. As type Ohms is a fixed point type, the operations include all of the standard arithmetic operators. To add two resistance values, we use the plus operator. However, because this operator is defined in package Common_Units, we must either prefix the plus operator with the package name or include a use clause to access the operator directly. A use clause makes all of the resources in the named package available without prefixing. A use type clause is more specific; it allows us to use operators¹ of the given type without prefixing.

# ### 3.2 Utility Packages

A utility package groups together the constants, types, subtypes, and subprograms necessary to provide some particular service. The library package Ada.Numerics.Elementary_Functions is a utility package that includes twenty-nine mathematical functions such as square root, trigonometric functions, and logarithms for Float values. There is also a generic version of this mathematical package that may be instantiated for any floating point type. Here is the declaration of a utility package that provides three operations for control over output displayed on a screen:

```
```ada
package Display_Control is

   procedure Bold_On;
   -- Everything sent to the screen after this procedure
   -- is called will be displayed in bold characters

   procedure Blink_On;
   -- Everything sent to the screen after this procedure
   -- is called will be blinking

   procedure Normal;
   -- Everything sent to the screen after this procedure
   -- is called will be displayed normally

end Display_Control;
```
```