# Retain count rules

There are a set of memory management conventions that all **Objective-C** programmers follow. If you are using ARC, it is following these conventions behind the scenes for you.

In these rules, I use the word “you” to mean “an instance of whatever class you are currently working on.” It is a useful form of empathy: you imagine that you are the object you are writing. So, for example, “If you retain the string, it will not be deallocated.” really means “If an instance of the class that you are currently working on retains the string, it will not be deallocated.”

Here, then, are the rules. (Implementation details are in parentheses.)

+   - If you create an object using a method whose name starts with **alloc** or **new** or contains **copy**, then you have taken ownership of it. (That is, assume that the new object has a retain count of 1 and is *not* in the autorelease pool.) You have a responsibility to release the object when you no longer need it. Here are some of the common methods that convey ownership: **alloc** (which is always followed by an **init** method), **copy**, and **mutableCopy**.
- An object created through *any* other means is *not* owned by you. (That is, assume it has a retain count of one and is already in the autorelease pool, and thus doomed unless it is retained before the autorelease pool is drained.)
- If you don't own an object and you want to ensure its continued existence, take ownership by sending it the message **retain**. (This increments the object's retain count.)
- When you own an object and no longer need it, send it the message **release** or **autorelease**. (**release** decrements the retain count immediately. **autorelease** causes the message **release** to be sent when the autorelease pool is drained.)
- As long as an object has at least one owner, it will continue to exist. (When its retain count goes to zero, it is sent the message **dealloc**.)

One of the tricks to understanding memory management is to think locally. The **Asset** class does not need to know anything about other objects that also care about its `label`. As long as an **Asset** instance retains objects it wants to keep, you won't have any problems. Programmers new to the language sometimes make the mistake of trying to keep tabs on objects throughout an application. Don't do this. If you follow these rules and always think local to a class, you never have to worry what the rest of an application is doing with an object.

Following the idea of ownership, now it becomes clear why you need to autorelease the string in your **description** method: The employee object created the string, but it doesn't want to own it. It wants to give it away.