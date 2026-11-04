In C#, a program can contain more than one thread of execution. When this is the case, the program is said to be multithreaded, and pieces of the program are executed concurrently. Thus, pieces of the program execute independently and simultaneously. This raises the prospect of a special type of problem: What if two threads try to use a resource that can be used by only one thread at a time? To solve this problem, you can create a critical code section that will be executed by one and only one thread at a time. This is accomplished by lock. Its general form is shown here:

```
```csharp
lock(obj) {
    // critical section
}
```
```

Here, obj is the object on which the lock is synchronized. If one thread has already entered the critical section, then a second thread will wait until the first thread exits the critical section. When the first thread leaves the critical section, the lock is released and the second thread can be granted the lock, at which point the second thread can execute the critical section.

> Note lock is discussed in detail in Chapter 23.

# readonly

You can create a read-only field in a class by declaring it as readonly. A readonly field can be given a value only by using an initializer when it is declared or by assigning it a value within a constructor. Once the value has been set, it can't be changed outside the constructor. Thus, a readonly field is a good way to create a fixed value that has its value set by a constructor. For example, you might use a readonly field to represent an array dimension that is used frequently throughout a program. Both static and non-static readonly fields are allowed.

> Note Although similar, readonly fields are not the same as const fields, which are described in the following section.

Here is an example that creates a readonly field:

```
```csharp
// Demonstrate readonly.

using System;

class MyClass {
  public static readonly int SIZE = 10;
}

class DemoReadOnly {
  static void Main() {
    int[] source = new int[MyClass.SIZE];
    int[] target = new int[MyClass.SIZE];

    // Give source some values.
    for(int i=0; i < MyClass.SIZE; i++)
      source[i] = i;
```
```