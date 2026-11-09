A programmer may desire that the control should ignore this “error,” and treat any value in this range as 0. This, however, is not possible, as there is no parameter to control this feature. But, this is only a theoretical possibility. It is unlikely that such a situation would ever arise in CNC-related calculations. An example of the theoretical possibility is given below:

```
```
#1 = .00000001;         (Assigns 10^-8 to variable #1)
#2 = #1 * #1 * #1 + #1; (The calculated value is 10^-24 which generates an alarm, as the value is smaller than 10^-99)
```
```

If such a situation is ever likely to occur, the programmer should normalize the “suspected” variable to 0, whenever its absolute value becomes smaller than, say, 10^-10. This will not have any adverse effect on the accuracy of further calculations because macro calculations are accurate up to only about eight decimal digits. A conditional statement such as the following can be used:

```
```
IF [ABS[#1] LT [0.00001 * 0.00001]] THEN #1 = 0;
```
```

Note that all the values lying in the permissible range cannot be displayed on the screen, which uses eight-digit decimal format. So, the minimum non-zero value (magnitude) that can be displayed is 0.0000001, and the maximum value is 99999999. The control displays nine stars (*********) as the value of a variable (on the macro variable screen) whenever its display is not possible, provided the value lies in the permissible range (magnitude lying between 10^-29 and 10^10).

# ### 3.5 System Variables

The term “system” refers to “CNC control.” So, system variables can also be called *control variables*. This is the last group of variables that are related to the current status of the CNC control.

# #### System Variables versus System Parameters

*System variables* should not be confused with system *parameters* (which are commonly referred to as just *parameters*). Parameters decide the default settings of the control. For example, as already discussed, the value of a certain parameter decides whether the bracket key on the MDI panel will give a parenthesis or a square bracket. *A parameter is not a variable.* We select a value for parameter to suit our requirement, and do not change it unless our requirement changes. On a new machine, all the parameters are factory-set, keeping in mind the most common applications. Normally, users do not need to change parameters. In fact, they should not, unless it is absolutely essential and the user clearly understands the effect of the change because an incorrect parameter setting may cause unexpected machine behavior.