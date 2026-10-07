
[content]
# CHAPTER 3: It's All About the Data

59

![](img/322e107ddf8f5cd963a6efafdcd86f38_67_0.png)

NSLog is a function that can take one or more parameters. The first parameter is generally the string that is to be printed to the console. The @ symbol in front of the string tells the compiler this is an Objective-C type string and not a C++ string. The @ is typically used in front of all your strings for iPhone apps. If you don't use the @ symbol, you will probably get a compiler error. NSLog is a very helpful function used by developers to test the execution of their code.

%d tells the compiler an integer will be printed and to substitute the value of the integer for the %d. See Table 3-5 for other NSLog formatting specifications. Finally, our second parameter is to be integer.

Figure 3-21 shows the completed executed output of our application.

To compile and run your application, click on the “Run” button on your toolbar. We can see that we printed out the NSLog string along with the notice at the end by the debugger seeing the app’s execution completed successfully.

> NOTE: If your editor doesn't have the same menus or gutter (the left-hand column that contains t line numbers of the program) you saw in the previous screenshots, you can turn these settings in the Xcode preferences. You can open the Xcode Preferences by clicking on the Xcode menu in the bar and selecting Preferences.

```objc
// main.m
// Chapter3

#import <Foundation/Foundation.h>

int main (int argc, const char * argv[]) {
    @autoreleasepool {
        // insert code here..
        int firstNumber = 1;
        int totalSum = 0;
        int firstNumber = firstNumber + 1;
        secondNumber = secondNumber + 1;
        totalSum = firstNumber + secondNumber;
        NSLog("The program has terminated successfully.");
    }
    return 0;
}
```

welcome to change it and/or distribute copies of it under certain conditions.
There is no limit on variety. Type "show copying" to see the conditions.
The GDB was configured as "x86_64-apple-darwin.tty" /dev/tty000
[Exited normally to process with result 0]
2021-09-08 23:57:02.162 Chapter3][7234:707] 7
2021-09-08 23:57:02.163 Chapter3][7234:707] 7 The program has terminated successfully.

Figure-31. Console log displaying the results of our Objective-C app

# Identifying Problems

Believe it or not, your program may not run the way you thought it would. The process of hunting down problems with your app is called debugging. In order to track down bugs in our apps, we can set breakpoints and inspect our variables to see the contents. To do this, simply click in the gutter where you want to set a breakpoint (see Figure 3-22). A breakpoint will stop our application from executing at that line and enable us to inspect our variables.

![](img/322e107ddf8f5cd963a6efafdcd86f38_69_0.png)

**Figure 3–22. Setting debugging "breakpoints"**

A blue pointer in the gutter of your editor denotes a breakpoint. When you run your application and your app hits a line of code that contains a breakpoint, your app will halt and display a blue line across the line of code with a breakpoint (see Figure 3–23). Additionally, you can inspect each variable by hovering over it with your mouse.

# CHAPTER 3: It's All About the Data

![](img/322e107ddf8f5cd963a6efafdcd86f38_70_0.png)

We will talk more about debugging your apps in Chapter 14.

## Summary

In this chapter, you learned about how data is used by our apps. You saw how to initialize variables and how to assign data to them. We explained that when variables are declared, they have a data type associated with them and that only data of the same type can be assigned to variables.

Finally, we showed you how to use variables in your first Alice app and finished by using variables with an Objective-C app.

## Exercises

- Write an Objective-C console app (Command-Line Tool) that multiplies two integers and displays the result to the console.
- Write an Objective-C console app that squares a float. Display the resulting float in the console.
- Write an Objective-C console app that subtracts two floats, with the result being stored as an integer. Note that rounding does not occur.

# Chapter 4

# Making Decisions About...and Planning Program Flow

One of the cool things about being an iPhone/iPad/Mac developer is we get to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

There is a downside to being developers: we have to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

There is a downside to being developers: we have to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

There is a downside to being developers: we have to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

There is a downside to being developers: we have to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

There is a downside to being developers: we have to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

There is a downside to being developers: we have to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

There is a downside to being developers: we have to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

There is a downside to being developers: we have to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

There is a downside to being developers: we have to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

There is a downside to being developers: we have to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

There is a downside to being developers: we have to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

There is a downside to being developers: we have to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

One of the cool things about being an iPhone/iPad/Mac developer is we get to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

There is the logic: we have to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

There is a downside to being developers: we have to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

One of the cool things about being an iPhone/iPad/Mac developer is we get to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

There is a downside to being developers: we have to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

There is a downside to being developers: we have to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

One of the cool things about being an iPhone/iPad/Mac developer is we get to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

There is a downside to being developers: we have to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

There is a downside to being developers: we have to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

Boolean logic is a system where binary operators like AND, OR, and NOT determine if conditions are met.

# CHAPTER 4: Making Decisions About...and Program Flow

One of the cool things about being an iPhone/iPad/Mac developer is we get to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

There is a downside to being developers: we have to tell exactly what we want them to do and it will be done—our devices will do tasks over and over again without getting tired. That's because iPhones/IPPads/Macs don't care how hard they worked yesterday, and they don't feel feelings in the way. These devices don't need hugs.

Binary operators take two operands. Unary operators take one operand.

## Boolean Logic

Boolean logic is a system where binary operators like AND, OR, and NOT determine if conditions are met.
