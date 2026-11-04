# Passing an Argument to a Thread

In the early days of the .NET Framework, it was not possible to pass an argument to a thread when the thread was started because the method that serves as the entry point to a thread could not have a parameter. If information needed to be passed to a thread, various workarounds (such as using a shared variable) were required. However, this deficiency was subsequently remedied, and today it is possible to pass an argument to a thread. To do so, you must use different forms of Start(), the Thread constructor, and the entry point method.

An argument is passed to a thread through this version of Start():

```
public void Start(object arg)
```

The object passed to arg is automatically passed to the thread’s entry point method. Thus, to pass an argument to a thread, you pass it to Start().

To make use of the parameterized version of Start(), you must use the following form of the Thread constructor:

```
public Thread(ParameterizedThreadStart entryPoint)
```

Here, entryPoint is the name of the method that will be called to begin execution of the thread. Notice in this version, the type of entryPoint is ParameterizedThreadStart rather than ThreadStart, as used by the preceding examples. ParameterizedThreadStart is a delegate that is declared as shown here:

```
public delegate void ParameterizedThreadStart(object arg)
```

As you can see, this delegate takes an argument of type object. Therefore, to use this form of the Thread constructor, the thread entry point method must have an object parameter.

Here is an example that demonstrates the passing of an argument to a thread:

```
// Passing an argument to the thread method.
using System;
using System.Threading;

class MyThread {
    public int Count;
    public Thread Thrd;

    // Notice that MyThread is also passed an int value.
    public MyThread(string name, int num) {
        Count = 0;

        // Explicitly invoke ParameterizedThreadStart constructor
        // for the sake of illustration.
        Thrd = new Thread(this.Run);

        Thrd.Name = name;

        // Here, Start() is passed num as an argument.
        Thrd.Start(num);
    }
}
```