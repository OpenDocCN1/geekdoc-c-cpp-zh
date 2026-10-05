Let's make another variable to play with.

```
to TestVar
local "Var1"
make "Var1 20
local "Var2"
make "Var2 50
show :Var1
show :Var2
end
```

What does your command center look like? It should show 20, then 50. But in this case, there are two mailboxes!

![](bbox=[0.105, 0.337, 0.61, 0.489])

There is a built-in procedure that is easy to use, sum. It takes 2 inputs, both numbers, and has one output (the answer). If you wanted to add 2 and 3, you would write sum 2 3, since outputs come after the procedure name. The answer you can show, or store in a variable, or whatever.

![](bbox=[0.039, 0.611, 0.196, 0.655])

Try this:

```
to TestVar
local "Var1"
make "Var1 20
local "Var2"
make "Var2 50
show :Var1
show :Var2
show sum 20 15
show sum :Var1 15
end
```