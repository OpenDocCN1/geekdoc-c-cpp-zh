# Setting Up the Environment

Figure 4-2: The security setting in the Tools/Options box.

![](bbox=[0.231, 0.115, 0.693, 0.345])

# Creating a template from a text file

The simplest TT file is just a text file, edited in Notepad, with some basic commands in it called Directives. Follow these steps to create a template from that basic text file:

+   1. Open Notepad.
2. In the new file, add the following lines of code.

```
<@## output extension=".cs" #>
public class TestClass
{
}
```

The lines are cryptic, I know, but they will make sense in a second.

+   3. Save the file in your Documents folder as GenerateClass.tt.
It should look like Figure 4-3.

![](bbox=[0.231, 0.698, 0.666, 0.922])

Figure 4-3: The world's simplest TT file.

Book IV
Chapter 4
Transforming Text Templates