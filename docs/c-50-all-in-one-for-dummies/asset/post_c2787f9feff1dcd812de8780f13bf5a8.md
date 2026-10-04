
![](img/6df7bb88e9302e98442acc219cfbd7fc_386_0.png)

```cs
using System;
using System.Windows.Forms;
namespace SimpleProgress
{
    public partial class Form1 : Form
    {
        // Declare the delegate. This one is void.
        delegate void UpdateProgressCallback();

        public Form1()
        {
            InitializeComponent();
        }
        // DoSomethingLengthy -- My workhorse method takes a delegate.
        private void DoSomethingLengthy(UpdateProgressCallback updateProgress)
        {
            int duration = 2000;
            int updateInterval = duration / 10;
            for (int i = 0; i < duration; i++)
            {
                Console.WriteLine("Something or other");
                // Update every tenth of the duration.
                if ((i % updateInterval) == 0 && updateProgress != null)
                {
                    updateProgress(); // Invoke the delegate.
                }
                if ( updateProgress != null ) updateProgress();
            }
        }
        // DoUpdate -- The callback method
        private void DoUpdate()
        {
            progressBar1.PerformStep();
        }
        private void button1_Click(object sender, EventArgs e)
        {
            // Instantiate the delegate, telling it what method to call.
            UpdateProgressCallback callback =
                new UpdateProgressCallback(this.DoUpdate);
            // Do something that needs periodic progress reports.
            // This passes a delegate instance that knows how to update the bar.
            DoSomethingLengthy(callback);
            // Clear the bar so that it can be used again.
            progressBar1.Value = 0;
        }
        private void button2_Click(object sender, EventArgs e)
        {
            this.Close();
        }
    }
}
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_386_1.png)

The class declaration is interesting as an aside:

```cs
public partial class Form1 : Form
```

The partial keyword indicates that this line is only part of the full class. The rest can be found in the Form1.Designer.cs file listed in Solution Explorer. (Take a look at it.) Later in the “Stuff Happens — C# Events” section, I revisit that file to show you a couple of things about “events.” Partial classes, which were introduced in C# 2.0, let you split a class between two or more files. The compiler generates the Form1.Designer.cs file, so don’t modify its code directly. You can modify it indirectly, however, by changing elements on the form. Form1.cs is your part.

# Tracking the delegate life cycle

Look at the example through the parts of the delegate life cycle:

- 1. You define the UpdateProgressCallback delegate near the top of the class:

```cs
delegate void UpdateProgressCallback();
```

Methods that this delegate can “point” to will be void, with no parameters. After the delegate keyword, the rest defines the signature of any method that the delegate can point to: its return type and the number, order, and types of its parameters. Delegates don’t have to be void — you can write delegates that return any type and take any arguments.

Defining a delegate defines a type, just as class Student {...} does. You can declare your delegate public, internal, protected, or even private, as needed.

It’s considered good form to append the name Callback to the name of a delegate type that defines a callback method, though C# couldn’t care less.

![](img/6df7bb88e9302e98442acc219cfbd7fc_387_0.png)

- 2. You instantiate the delegate and then pass the instance to the DoSomethingLengthy() method in the button1_Click() method:

```cs
UpdateProgressCallback callback =
    new UpdateProgressCallback(this.DoUpdate); // Instantiate the delegate.
DoSomethingLengthy(callback); // Pass the delegate instance to a method.
```

This delegate “points” to a method on this class (and this is optional). To point to a method on another class, you need an instance of that class (if the method is an instance method), and you pass the method like this:

```cs
SomeClass sc = new SomeClass();
UpdateProgressCallback callback =
    new UpdateProgressCallback(sc.DoUpdate);
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_387_1.png)

But if the method is a static method (located anywhere), pass it like this:

```cs
UpdateProgressCallback callback =
    new UpdateProgressCallback(SomeClass.DoUpdate);
```

What you're passing in the instantiation is just the method's name, no parameters. What you pass to DoSomethingLengthy() is the delegate instance, callback (which points to the method).

# 3. Your DoSomethingLengthy() method does some "lengthy processing" and periodically pauses to call back to the form so that it can update its progress bar.

Invoking the delegate inside DoSomethingLengthy() looks like calling a method, complete with parameters, if any:

```cs
updateProgress(); // Invoke the delegate instance passed in.
```

DoSomethingLengthy() looks like this:

```cs
private void DoSomethingLengthy(UpdateProgressCallback updateProgress)
{
    int duration = 2000;
    int updateInterval = duration / 10; // Every 200 milliseconds
    for (int i = 0; i < duration; i++)
    {
        Console.WriteLine("Something or other");
        // Update the form periodically.
        if ((i % updateInterval) == 0 && updateProgress != null)
        {
            updateProgress(); // Invoke the delegate.
        }
        if(updateProgress != null) updateProgress();
    }
}
```

The "lengthy process" doesn't do much. It sets the duration variable to 2,000 loop iterations — a few seconds at runtime, which is more than enough for this demo. Next, the method computes an "update interval" of 200 iterations by dividing the overall duration into tenths. Then the for loop ticks off those 2,000 iterations. For each one, it checks whether it's time to update the user interface, or UI. Most times through the loop, no update occurs. But whenever the if condition is true, the method invokes the UpdateProgressCallback instance that was passed.

# 4. When the if condition is true, the method invokes the UpdateProgressCallback instance that was passed. Always check a delegate for null before invoking it.

# 5. When the delegate is called, it invokes the method you pointed at — in this case Update():

```cs
private void DoUpdate()
{
    progressBar1.PerformStep();
}
```

# 6. Finally, the loop runs, DoSomethingLengthy() exits, returning control to button1_Click(). That method then clears the ProgressBar by 0.

![](img/6df7bb88e9302e98442acc219cfbd7fc_389_0.png)

And there you have it. Using the delegate to implement a callback, the program keeps its progress bar up to date. See the list of uses for delegates in the section "I delegated the example." Write a custom delegate when you need to define a type for delegate-type parameters. Use predefined delegates for events and the collection classes' Find() and ForEach() methods.

# Shh! Keep It Quiet — Anonymous Methods

After you have the gist of using delegates, take a quick look at Microsoft's first cut at simplifying delegates in C# 2.0 a couple of years ago.

![](img/6df7bb88e9302e98442acc219cfbd7fc_389_1.png)

To cut out some of the delegate rigmarole, you can use an anonymous method. Anonymous methods are just written in more traditional notation. Although the syntax and a few details are different, the effect is essentially the same whether you use a "raw" delegate, an anonymous method, or a lambda expression. You can find out more about lambda expressions on http://csharp102.info.

An anonymous method creates the delegate instance and the method it "points" to at the same time — right in place, on the fly, tout de suite. Here are the guts of the DoSomethingLengthy() method again, this time rewritten to use an anonymous method (boldfaced):

```cs
private void DoSomethingLengthy() // No arguments needed this time.
{
...
for (int i = 0; i < duration; i++)
{
    if ((i % updateInterval) == 0)
    {
        UpdateProgressCallback anon = delegate() // Create delegate instance.
        {
            progressBar1.PerformStep();          // Method 'pointed' to
        };
        if(anon != null) anon();                // Invoke the delegate.
    }
}
```
