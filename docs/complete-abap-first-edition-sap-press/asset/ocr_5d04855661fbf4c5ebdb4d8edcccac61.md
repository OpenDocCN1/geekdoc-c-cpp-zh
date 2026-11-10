| Attribute | Explanation |
|---|---|
| Fixed Point Arithmetic | If this attribute is set for a program, the system rounds type p fields according to the number of decimal places, or pads them with zeros.<br>The decimal sign in this case is always the period (.), regardless of the user's personal settings. SAP recommends that this attribute is always set. |
| Unicode Checks Active | This attribute allows you to set if the syntax checker should check for non-Unicode-compatible code and display a warning message.<br>As of SAP NetWeaver 7.5, the system does not support non-Unicode systems, so this option is always selected by default. |
| Start Using Variant | Applicable only for executable programs. If you set this attribute, other users can only start your program using a variant. You must then create at least one variant before the report can be started. |

**Table 4.6** Program Attributes (Cont.)

+   4. Under the **Attributes** section, provide the following values (see **Figure 4.19**):
+      - Type: Executable program
+      - Status: Test Program
+      - Application: Unknown application
+      - Also check the Unicode Checks Active and Fixed Point Arithmetic checkboxes.

Click the **Save** button when finished.

![](bbox=[0.143, 0.67, 0.772, 0.844])

**Figure 4.19** Maintaining Program Attributes