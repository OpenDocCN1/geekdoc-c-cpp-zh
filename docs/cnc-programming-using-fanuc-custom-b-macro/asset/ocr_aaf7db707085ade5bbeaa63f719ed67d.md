+   3. Find out the feedrate active in the block, immediately preceding the macro calling block.
+   4. If the G01 block does not contain an F-word, use the feedrate obtained in the previous step.
+   5. Find out the S-word value active in the immediately preceding block.
+   6. If the G01 block does not contain an S-word, use the value obtained in the previous step.
+   7. Find out the tool number using FIX(T-code value/100), which extracts the left-most two digits from the four-digit (can be a three-digit number also) T-code value. For example, 0102 (corresponding to T0102) would give 01, as the current tool number.
+   8. If the tool number is not 7, go to step 15.
+   9. Find out whether G96 or G97 is active at the time of calling the macro.
+   10. Find out the rpm at the time of calling the macro (i.e., in the immediately preceding block). In G97 mode, it would be equal to the S-word value. In G96 mode, calculation using the given formula would be needed.
+   11. Specify the maximum permissible feedrate (Fₘₐₓ) in millimeters per minute.
+   12. Convert Fₘₐₓ to be in millimeters per revolution if G99 is active, using the formula:
+   
+       feed per minute = feed per revolution × rpm
+   
+   13. Convert Fₘₐₓ to be in inches per minute or inches per revolution, if G20 is active, by dividing it by 25.4.
+   14. If the specified/previous feedrate is greater than Fₘₐₓ, use Fₘₐₓ as feedrate.
+   15. Execute linear interpolation with specified/previous values of X, Z, U, W, and S, and appropriate value of F.
+   16. Return to the calling program.

```
O9012 (REDEFINES G01 ON LATHE);
#100 = #4005;          (Stores 98 or 99, corresponding to G98
                       and G99, respectively, whichever was
                       active at the time of calling the macro.
                       This information is needed because one
                       must know whether the specified feedrate
                       in the macro calling block is in feed per
                       minute or feed per revolution. Step 1
                       complete)
```