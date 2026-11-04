# Revisiting the switch Statement

Code often has to dispatch to certain logic based on an enum value. One of the best candidate statements to carry out this task is the switch statement. In fact, the code editor in Visual Studio has a handy feature for generating a full switch statement for all of an enum's members. Here's the way to do it: Given a variable of an enum type, type switch and press Tab twice. Now enter the variable name and press Enter. For our Color type, this technique is illustrated in Figure 11.10.

![](bbox=[0.14, 0.36, 0.68, 0.7])

FIGURE 11.10 Generating a switch statement for an enum.

Although it might seem tempting to get rid of the default branch, this isn't a good idea because enums can carry undefined values, as discussed previously. Put some proper code in there that raises a runtime exception to guard against unknown values. Also, if your code is to return something based on an enum value, you won't get away with omitting the default branch due to the language's definite assignment rules ("all code paths need to return a value").

You can also use regular if statements to carry out specific actions based on an enum's value. However, when there are a lot of cases to look for, the switch statement is almost certainly the better choice, both for code readability and efficiency of execution.

# Behind the Scenes

To wrap up our discussion about enums, let's take a quick peek behind the scenes. Even though the use of the colon syntax to specify an underlying type makes it seem like the enum type derives from the underlying type, this is not the case. All enum types derive from the System.Enum base type that's supplied by the runtime. Each member defined on the enum turns into a constant field. An instance of the enum contains a single field holding the value that's being used. Figure 11.11 shows what an enum definition looks like in ILDASM.