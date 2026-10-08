# Pass Me the Code, — Examples 361

+   More generally, to customize a method: The method you're customized provides a framework, and its caller supplies a delegate to do the work. "Honey, this grocery list to store and follow it exactly." The delegate method carries out a task that the customized method needs done (but can't handle by itself). The customized method is responsible for invoking the delegate at the appropriate moment.

![](bbox=[0.118, 0.143, 0.203, 0.218])

# First, a simple example

The SimpleDelegateExample on the Web site demonstrates a simple delegate:

```
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
```

![](bbox=[0.118, 0.325, 0.203, 0.405])

The delegate-related parts of this example are highlighted in boldface.