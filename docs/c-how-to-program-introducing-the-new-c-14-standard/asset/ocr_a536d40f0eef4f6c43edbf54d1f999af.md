# Section 13.6 Stream Manipulators:  
A Deeper Look

+   - To change the base in which integers output, use the manipulator `hex` (p. 588) to set the base to hexadecimal (base 16) or `oct` (p. 588) to set the base to octal (base 8). Use manipulator `dec` (p. 588) to reset the base to decimal. The base remains the same until changed explicitly.
+   - The parameterized stream manipulator `setbase` (p. 588) also sets the base for integer output. `setbase` takes one integer argument of `10`, `8` or `16` to set the base.
+   - Floating-point precision can be controlled with the `setprecision` stream manipulator or the `precision` member function (p. 588). Both set the precision for all subsequent output operations until the next precision-setting call. The `precision` member function with no argument returns the current precision value.
+   - Parameterized manipulators require the inclusion of the `<iomanip>` header.
+   - Member function `width` (p. 590) sets the field width and returns the previous width. Values narrower than the field are padded with fill characters. The field-width setting applies only for the next insertion or extraction, then input is performed using the default settings. Values wider than a field are printed in their entirety.