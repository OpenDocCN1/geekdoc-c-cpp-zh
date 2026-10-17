```
statement;
statement;
break;
case expression:
statement;
break;
default:
statement;
}
```

Lets disintegrate the above format and study the different parts. The first statement is the switch statement followed by a pair of parentheses in which the word “choice” is given. This accepts the choice that the user makes. The case can be baptized only with either integers or characters nothing else (not even floating point).

+   - **Example 3.2:**
+     - case1
+     - case2
+     - case3 or
+     - case a
+     - case b
+     - case c

Based on the choice that the user makes the executable statement in that particular case is activated. The next thing to be discussed is the “case.” within each of these is the options to be performed specified. each case has a particular set of statements to be executed. Whenever a particular case is selected the statements in the case are executed.

The break has already been discussed but the efficiency of the break can be best noticed in the switch statements. you have noticed that the break statements are used at the end of each case. This is done because it notifies the control that once the case has been executed the control should not proceed any further.

The default takes charge when the option entered by the user does not match with the given case. When no match is found with any of the given case the statements in the default are executed.