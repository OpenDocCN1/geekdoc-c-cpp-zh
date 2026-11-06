of the diagram by not showing how the Cook object does this.) The result of this comes back as either true or false, which we store in the `h` symbol. Then, in the next step, the Server calls `prepareFood("French fries")` only if `h` is true. That’s what the brackets with the `h` in them mean.

Finally, if `h` is true, the Server object returns the order of fries in the form of a new `Food` object. This is the return line that starts with `[h]`, which means that `h` is true. (We don’t show the process of the Cook creating the Food object; you can see that kind of thing in Figure 4-3.) But if `h` is not true, the Server object returns a symbol indicating that there are no more French fries. (You will probably make this symbol an enum in C++, or perhaps a 0.)

![](bbox=[0.238, 0.346, 0.787, 0.634])

**Figure 4-7:**  
To show conditions and comparisons, use brackets.

![](bbox=[0.119, 0.669, 0.204, 0.741])

At this point, we’re actually getting into some local variable names, such as the value of whether there are French fries. However, most CASE tools aren’t sophisticated enough to take a sequence diagram such as this and generate C++ code that works. Most can generate some basic code, and some let you type the code by using the CASE tool. You will most likely use this diagram as a guide to write your own code. Designing it through the diagram is a lot easier than with the code. And other people—those who *don’t program*—can get a basic idea of the flow of events by looking at the sequence diagram. It’s less likely that they would understand code. That way, the *stakeholders* (anyone who has a vested interest in the application, which includes both management and users) can look at the diagram and tell you whether you’re building what they want you to build. Often, the level and type of stakeholder participation affects the viability of your application and determines whether people actually use it, so getting stakeholder feedback is essential to the success of your programming efforts.

![](bbox=[0.882, 0.323, 0.999, 0.491])