With these additions we now have a script that will bring up a fairly complete GUI. Unfortunately, it still does not do anything yet. We will get to that soon enough.

# ### 11.2.5 Tooltips

You have probably seen GUIs where, if you leave the mouse hovering above something for a while, a message will pop up telling you something about what it does. These are called **TOOLTIPS**. All the components have a field in them called `tooltip` that is a `String`. You can set the `tooltip` to be a message that you want to pop up. This will happen automatically if the user leaves their mouse pointer over that component for a period of time.

# ## 11.3 Basic Interactivity

The GUI that we have created for our recipe book looks fine and has all pieces that we need. Unfortunately, it does not do anything at this point. In order to make it interactive, we need to code that in. Interactivity in GUIs is significantly different from that in console programs. For a console program, the only real input is to have the user type in information. We were able to read that information using functions like `readInt()`, `readLine()`, `readDouble()`, etc. Similarly, the only output was to print things back to the console. In addition, while the user was typing stuff in, the program was supposed to be paused. We describe this by saying that user input is BLOCKING. So nothing else was happening when we called `readLine()`. That call would block the execution and it would not continue until the user had entered something.

When you move to a GUI environment, all the rules of interactivity change. There are now multiple components that the user can interact with. Each one might respond in different ways. For example, a `Button` can just be clicked. On the other hand, a `TextField` can have the user type into it and you need to know when they are done. Each different component has different ways the user can interact with them, and each of them needs to be waiting for the user to interact. No single component can block execution while it waits for the user. They all have to be active at the same time.

This section looks at the way we do user input in a GUI built with the `scala.swing` library.

# ### 11.3.1 Partial Functions

There is one feature of the Scala language that we have not talked about before that is required for doing interactions in GUIs: the PARTIAL FUNCTION. The idea of a partial function comes from mathematics. It is a function that can only operate on certain values of the arguments and is undefined for other arguments. The syntax for partial functions in Scala is basically like having a `match` expression without the argument and the `match`. You simply have curly braces with different `cases` inside of them.

```
```
{
  case 1 => // code goes here
  case 2 => // code goes here
}
```
```