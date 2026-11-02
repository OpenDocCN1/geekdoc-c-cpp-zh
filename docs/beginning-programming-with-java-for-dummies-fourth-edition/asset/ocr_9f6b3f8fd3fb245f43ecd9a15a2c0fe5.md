Figure 7-8
A run of the preincrement code
(the code in Figure 7-7).

![](bbox=[0.27, 0.17, 0.48, 0.36])

The double plus sign goes under two different names, depending on where you put it. When you put the ++ before a variable, the ++ is called the preincrement operator. In the word preincrement, the pre stands for before. In this setting, the word before has two different meanings:

+   - You're putting ++ before the variable.
+   - The computer adds 1 to the variable's value before the variable is used in any other part of the statement.

Figure 7-9 has a slow-motion, instant replay of the preincrement operator's action. In Figure 7-9, the computer encounters the System.out.println(++gumballs) statement. First, the computer adds 1 to gumballs (raising the value of gumballs to 29). Then the computer executes System.out.println, using the new value of gumballs (29).

Figure 7-9
The preincrement operator in action.

![](bbox=[0.22, 0.68, 0.9, 0.85])

# Using postincrement

An alternative to preincrement is postincrement. With postincrement, the post stands for after. The word after has two different meanings:

+   - You put ++ after the variable.
+   - The computer adds 1 to the variable's value after the variable is used in any other part of the statement.