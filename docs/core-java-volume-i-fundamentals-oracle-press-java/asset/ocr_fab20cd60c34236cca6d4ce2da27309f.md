Suppose you wrote your program and made it bulletproof by catching and properly handling all exceptions. Then you run it, and it does not work right. Now what? (If you never have this problem, you can skip the remainder of this chapter.)

Of course, it is best if you have a convenient and powerful debugger. Debuggers are available as a part of professional development environments such as Eclipse, IntelliJ, and NetBeans. In this section, I offer a number of tips that may be worth trying before you launch the debugger.

+   1. You can print or log the value of any variable with code like this:

```
```
System.out.println("x=" + x);
```
```

or

```
```
Logger.getGlobal().info("x=" + x);
```
```

If x is a number, it is converted to its string equivalent. If x is an object, Java calls its toString method. To get the state of the implicit parameter object, print the state of the this object.

```
```
Logger.getGlobal().info("this=" + this);
```
```

Most of the classes in the Java library are very conscientious about overriding the toString method to give you useful information about the class. This is a real boon for debugging. You should make the same effort in your classes.

+   2. One seemingly little-known but very useful trick is putting a separate main method in each class. Inside it, you can put a unit test stub that lets you test the class in isolation.

```
```
public class MyClass
{
   methods and fields
   . . .
   public static void main(String[] args)
   {
      test code
```
```