# 188 Plug-In JavaScript: 100 Solutions

If it does, the local string temp is created and the calls array is iterated through the local variable j as an index into it. This is done because the chain keeps repeating to continually pass an entire chain as a single statement of a new chain. To understand this, consider the following pseudocode:

```
if expr is true...
Add this statement to a chain
Also add this statement
And then this statement
Now all of add including the if statement to the chain
```

What is happening here is the same as what the code in the While() plug-in does. It first evaluates expression and if it is true it sends all the statements it has been passed to the Chain() plug-in. It then sends all of the preceding statements, so that when the first sequence has finished executing, the if statement and associated calls will come up once and be passed once over the While() plug to deal with.
The next time if expr evaluates to false, the Will() plug-in will finish. But if it evaluates to true, all the statements are sent to Chain(), followed by all code required to start over again. And so the process continues, going round and until expr evaluates to false, if ever.

# How the Additional Call to While() Is Added to a Chain

In went, the proceeding adds a call to While() as one of the items in a chain. To do this, each element is extracted from the array and appended to the string temp. This is because the Chain() plug-in, which will be later, does not accept array that are themselves arrays. Instead, elements must be a string value that will be converted into an array by a call to eval() (by the NextChain() plug-in, which occurs when the statement's turn to execute). The code creates temp is as follows:

```
var temp = ''
for (var j = 0; j < calls.length; ++j)
temp = '' + calls[j].replace(/"/g, "\\\") + '','
```

Each round the value in calls[j] is extracted, the replace() function is used to escape double quotes, changing them from " to \" . Because a double quote is also added to the start and end of each string section (by a comma), any double quotes that appear in the strings and are not escaped will clash with the outside quotes and a syntax error, in a way that the following statement would:

```
string = "She said "Hello"
```

The correct version of this statement with double quotes is:

```
string = "She said \"Hello\"
```

# The Assembled String

Let's assume calls contains the following two strings:

```
FadeOut('obj', 50, 0)
FadeIn("Obj", 50, 0)
```