and the Stack Trace. With message, we just get the error text.

+   3 There were no changes to kill. It’s just here for reference so we can see the error message that it will pass, which will show up in the program’s output.

+   4 Using runAff so we can add a Canceler.

+   5 logEverySecond never exits since it only gets canceled, which means that this case will never be called. const $ pure unit is here just to make the Type Checker happy.

+   6 cancelWith is flipped since it’s first Parameter is an Aff a, which, in this case, is logEverySecond.

+   7 The Canceler Function will display the error message by using message on Error as opposed to displaying the whole Stack Trace via show.

This program’s output is:

```
0
1
2
File contents: "This is a test.\n"
3
4
Killing you softly...
```

# 22.2.3. AVars

Imagine you have a Fiber that reads a File and you want that data to be processed by another Fiber.

We can accomplish this by using a mechanism called an AVar, which stands for Asynchronous Variable.

An AVar is an Asynchronous Variable that can contain data, or can be empty. A Fiber can read and write to the AVar and even block until data becomes available.

To see how one might use AVars let’s write a program that runs 2 Fibers, one, which reads a File and sends it to the other via an AVar: