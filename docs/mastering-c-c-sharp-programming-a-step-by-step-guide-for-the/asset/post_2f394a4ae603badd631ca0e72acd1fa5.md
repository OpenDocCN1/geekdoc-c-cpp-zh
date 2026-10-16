
out the thread; that thread will be paused and the next thread will go in and get an object to update and our index hasn’t been updated so the new thread grabs the object that the previous thread had. That means that a specific object will be updated twice.

It doesn’t end there. Now the second thread will change that index to the next object so the third thread will get the correct object when it requests work. That leaves the second thread to carry on with its own updating work. While all this is going on, the operating system makes yet another switch and now our first thread is back in the mix again. This thread already knows which of the objects needs to be updated - the one at index 0 but thread 2 is also updating this. The first thread moves on and it moves the index again, onto 2 so the next object (1) is skipped over completely. One is updated twice while another is skipped altogether.

There is one main underlying issue – we have two different threads each trying to get access to or change the same data and neither has checked that it is safe to do this. This can be fixed. There is a way to mark bits of code and ensure that one thread can access that section at any one time. We call this thread-safety. If a thread reaches the section of code while another one is in it, it will need to wait until the first thread has gone.

This can slow things down quite a bit but the upside is you have consistent data. If your code doesn’t need to be made thread-safe, don’t do it, but when you do need it, make sure you do it.

Let’s discuss how to make your code thread-safe. We will need two pieces of code for this. When a thread is getting ready to go into a piece of code that has to be thread-safe, we use a different keyword – lock. With this, we also need to have an object to lock on. The easiest way is to lock on an instance variable marked as private so you should go ahead and add one where the method that has to be thread-safe is in your main thread controller class:

```
private object threadLock = new object();
```

If thread-safety is needed across all the class instances, this can also be created as a static variable rather than an instance variable.

```
private static object threadLock = new object();
```

I don’t need to tell you that you can name your variable whatever you want; I use threadLock for the sake of simplicity.

To use the threadLock object to make a code block safe, you would add code like this:

```
lock(threadLock)
{
// The code here is now thread-safe.
// We can only have one thread in here at a time.
// The other threads will need to wait
// at the "lock" statement.
}
```

## Quick Primer

- Threading lets you run several sections of code at the same time.

- C# makes it easy to start a new thread: Thread thread = new Thread(MethodNameHere); thread.Start().

- Whatever method you use, it must have the void return type and it cannot take parameters. If you want a thread to return information or you want it to pass parameters in, you need to make an object that contains the information you want as properties or instance variables and one method that have a void return type and no parameters for the thread to run in.

- You can use the Join method to wait for threads to finish:

```
thread.Join().
```

- Use the lock keyword if you need to make a section of code thread-safe: lock(aPrivateObject) {/* the code here is thread-safe */}. Usually, if the code you want to make thread-safe is all inside one class, a private instance variable is needed. If you need to make all class instances thread-safe, use a private static variable.

## What's Next?

Threading is quite a complex feature and isn’t all that easy to learn. Not all programs will need it and sometimes, you will be using a framework, such as WinForms, XNA, or WPF, that takes care of thread-safety behind the scenes. But, when you need to use it, at least now you will have a basic understanding of how it works and how to do it.

Next, we are going to look at something that is quite important in C# - operator overloading.

## Operator Overloading

So far, throughout this guide, we’ve seen and used many different operators. Each has its own functionality built-in that will do specific things. Most of the time, these operators and their functions are defined by standard math although there are one or two that do some not-so-standard stuff – the + operator, for example, used for concatenating or adding two strings together. There is no way to do that in standard math but there is in C#.

When you create a class in C#, you can define the way the operators work with the class. For example, if you created an object called ‘Burger’, you could use the + operator to add a pair of Burger objects together and you also can determine exactly what it means. We call this operator overloading and it is one of the nicest C# features. Those of you who have a programming background will already know that, and you can also do operator overloading in C++, but you can’t do it in Java.

Not all operators can be overloaded. For example, you cannot overload the assignment (=) operator; it isn’t possible for you to define what that operator does and that’s no bad thing – you could cause all sorts of problems if you could!

Lots of them can be overloaded and you’ll obviously want to know which ones. These are the most common ones that you will use all of the time:

- +
- -
- *
- /
- %
- ++
- --
- ==
- !=
- >
- <
- >=
- <=

There are some others including +=, -=, *=, /=, and %=. However, when the + operator is overloaded, it will automatically overload the += operator.

You should also know that when you overload a relational operator, you must do them in pairs. If the == operator is overloaded, so must the != operator be overloaded. And if the > operator is overloaded, you also need to overload the < operator, and so on.

We mustn’t forget that some of the operators have two versions – unary and binary. Take the + operator, for example. The binary version will do operations on two things, for instance, adding 4 + 6 – the operator will apply to both numbers separately. The unary operator, on the other hand, will only do operations on one thing. Take -9 for example; the operator is only applied to the 9, no other number.

What can’t be overloaded?

- &&
- ||
- =
- . (dot operator)
- new
- and a few others that we haven’t looked at.

The [ and ] operator, which is used for indexing, may be overloaded by using indexers, but we will come onto that in the next section.

## Overloading Operators

Operators can be overloaded for any class that you want, but to keep things relatively simple here, I will choose a class that actually makes sense from the overloading perspective. We’ll use the Point class to do the overloading – this stores two coordinates of X and Y. If you understand vectors from physics and math then this will make some sense to you.

Let’s begin with a basic class:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace OperatorOverloading
{
    public class Vector
    {
        public double X { get; set; }
        public double Y { get; set; }

        public Vector(double x, double y)
        {
            X = x;
            Y = y;
        }
    }
}
```

If you think back to your school days when you did math and physics, you will remember that two vectors can be added together. When you do this, you get another vector as the result, adding the X and Y components.

Overloading the + operator means adding the following code to the class called Vector:

```
public static Vector operator +(Vector v1, Vector v2)
{
    return new Vector(v1.X + v2.X, v1.Y + v2.Y);
}
```

No matter what one it is, every operator overload must be static and public and that should make sense to you; we want to be able to access the operator in the code and it doesn’t just belong to a class instance; it belongs to the entire class.

The next thing we do is specify what return type we want; in our case, this will be Vector. The operator keyword is used together with the specific operator we want to overload, which is the + operator. Next, we have two parameters, one for each side of the operator.

```
public static Vector operator -(Vector v)
{
    return new Vector(-v.X, -v.Y);
}
```

We can also have several versions of one operator:

```
public static Vector operator +(Vector v, double scalar)
{
    return new Vector(v.X + scalar, v.Y + scalar);
}
```

Now we can add a vector and a scalar together, which is nothing more than a plain number, something that simply doesn’t make sense from a standard math perspective.

We can overload the relational operators the same way but the return must be a bool:

```
public static bool operator ==(Vector v1, Vector v2)
```
