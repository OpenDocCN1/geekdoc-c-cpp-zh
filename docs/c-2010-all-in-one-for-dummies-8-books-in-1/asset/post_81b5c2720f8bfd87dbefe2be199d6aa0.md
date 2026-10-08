
# Pass Me the Code, — Examples 361

- More generally, to customize a method: The method you're customized provides a framework, and its caller supplies a delegate to do the work. "Honey, this grocery list to store and follow it exactly." The delegate method carries out a task that the customized method needs done (but can't handle by itself). The customized method is responsible for invoking the delegate at the appropriate moment.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_386_0.png)

# First, a simple example

The SimpleDelegateExample on the Web site demonstrates a simple delegate:

```c
// SimpleDelegateExample -- Demonstrate a simple delegate callback.
using System;
namespace SimpleDelegateExample
{
    class Program
    {
        delegate void MyDelegate(string name); // Inside class or namespace
        static void Main(string[] args)
        {
            // Create a delegate instance pointing to the CallBack method.
            // Note that the callback method is static, so you prefix the name
            // with the class name, Program.
            MyDelegate del = new MyDelegate(Program.CallBack);
            // Call a method that will invoke the delegate.
            UseDel(del, "hello");
            // Wait for user to acknowledge results.
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
        // A "workhorse" method that takes a MyDelegate delegate
        // argument is a string I want to pass
        // to the delegate invocation.
        private void UseDel(MyDelegate delegate, string arg)
        {
            if (delegate == null) // Don't invoke null delegate!
            // Here's where you invoke the delegate.
            // What's written here? A return representing the length of arg.
            Console.WriteLine("UseDel writes {0}", arg);
        }
        // Callback A method that conforms to the MyDelegate
        // delegate signature (takes a string, returns an int).
        // The delegate will call this method.
        public static int CallbackMethod(string stringPassed)
        {
            // Let's see what you get here.
            // What's written here? stringPassed.
            Console.WriteLine("CallbackMethod writes: {0}", stringPassed);
            // Return an int.
            return stringPassed.Length; // Delegate requires an int return.
        }
    }
}
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_386_1.png)

The delegate-related parts of this example are highlighted in boldface.

# 362 A Real-World Example

In that setup, the sequence of events:

1. UseTheDel() takes two arguments, a MyDelType delegate, and a string that it calls arg. So, when Main() calls UseTheDel, it passes my delegate instance to be used inside the method. When I created the delegate instance, del, in Main(), I passed the name of the CallbackMethod() as the method to be called. Because CallbackMethod() is static, I had to prefix the method with the class name, Program. I tell you more about it in this chapter.
2. UseTheDel(), the method ensures that the delegate isn't null and starts a WriteLine() call. When that, before it finishes, the method invokes the delegate by calling del(arg). arg is something you can pass to the delegate, which causes the CallbackMethod() to be called.
3. CallbackMethod(), the method writes its own message, including the string that was passed when UseTheDel() invoked the delegate. Then CallbackMethod() returns the length of the string it was passed, and that length is written out as the last part of the WriteLine() in UseTheDel().

The output looks like this:

```
CallbackMethod writes: hello
UseTheDel writes 5
Press Enter to terminate...
```

UseTheDel() phones home and CallbackMethod() answers the call.

# A Real-World Example

For a more realistic example than SimpleDelegateExample, I show you how to write a little app that puts up a progress bar and updates it every time a lengthy method invokes delegate.

# Getting an overview of the bigger example

The SimpleProgress example on the Web site demonstrates the Windows Forms control that I discuss at the top of this chapter. (By the way, SimpleProgress is a small example). The SimpleProgress example shows a window with two buttons and a progress bar. In this example, you'll see how the progress bar updates as you click the buttons.

The SimpleProgress example shows a window with two buttons and a progress bar. In this example, you'll see how the progress bar updates as you click the buttons.

# 364 A Real-World Example

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_389_0.png)

In this simple example, you're putting all code in the form. Now, in design mode, add a handler method for each button:

1. On the form, double-click the new button. This action generates a method in the code behind. It looks like this—when you bold the code:

```csharp
private void button2_Click(object sender, EventArgs e)
{
    this.Click(); // 'this' refers to the Form class.
}
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_389_1.png)

2. Double-click the new Click to Start button to generate its handler method, which looks like the following in the code-behind:

```csharp
private void button1_Click(object sender, EventArgs e)
{
    UpdateProgressBar callback = UpdateProgressBar(this);
    DoUpdate();
    // Do something that needs progress reports.
    // This passes a delegate instance that knows how to update the bar.
    DoSomething(callback);
    // Clear the bar so that it can be used again.
    progressBar.Value = 0;
}
```

3. Add the following DoUpdate() method to the form class:

```csharp
private void DoUpdate()
{
    progressBar.PerformStep(); // Tells progress bar to update itself
}
```
