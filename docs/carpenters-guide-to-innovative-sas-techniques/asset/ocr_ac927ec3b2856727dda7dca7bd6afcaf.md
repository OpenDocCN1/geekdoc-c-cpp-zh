| Option | Option Abbreviation | Example Value | What It Does |
|---|---|---|---|
| height= | h= | 10pct | sets size to 10 percent |
| color= | c= | cxdedede | sets color to a shade of gray |
| font= | f= | Arial | sets the font to ARIAL |
| 'text string' |  | 'Units are mg' | assigns a text string to the option |

The first layer of options control major aspects of the axis. These include such things as:

+   - ORDER= range of values to be included
+   - LABEL= axis label
+   - VALUE= tick mark control
+   - MAJOR= major tick marks (the ones with text)
+   - MINOR= minor tick marks

When building an AXIS statement, parentheses are used to form groups of sub-options, and indenting to each level of option can be helpful in keeping track of which options go with what.

```
```
axis2 order =(3 to 6 by 1) ❶
   label =(h=2 ❷
          font='Times New Roman' ❸
          "Potassium Levels") ❹
   minor =(n=1) ❺
          angle=90 ❻
          rotate=0 ❺ ;
axis1 minor=(n=4) ❺
      color=black
      label=("BMI")
      order=(15 to 40 by 5);
```
```

This is a fairly typical AXIS statement. Notice that the values of options are in parentheses. This allows you to specify the sub-options.

+   - ❶ ORDER= Restricts the axis range; data can be excluded. Here the range of the axis is limited to values between 3 and 6 with major tick marks at the integers. The VALUE= option (shown in the LEGEND example) specifies the attributes of the major tick marks.
+   - ❷ H= sets the height of the label's text to 2 units (the default units are cells).
+   - ❸ FONT= specifies the font. Fonts with multiple words should be quoted.
+   - ❹ 'text' specifies the text for the label, which overrides the variable's label.
+   - ❺ MINOR= specifies the number of minor tick marks. The keyword NONE can be used to turn off minor tick marks.

![](bbox=[0.22, 0.536, 0.647, 0.773])

+   - ❻ ANGLE= rotates the entire label 90 degrees (from horizontal to vertical). Angle=0 is horizontal.