of the anonymous method and is now the preferred approach to creating an anonymous function. However, anonymous methods are widely used in existing C# code. Therefore, they are still an important part of C#. Furthermore, anonymous methods are the precursor to lambda expressions and a clear understanding of anonymous methods makes it easier to understand aspects of the lambda expression. Also, there is a narrow set of cases in which an anonymous method can be used, but a lambda expression cannot. Therefore, both anonymous methods and lambda expressions are described in this chapter.

# Anonymous Methods

An anonymous method is one way to create an unnamed block of code that is associated with a specific delegate instance. An anonymous method is created by following the keyword delegate with a block of code. To see how this is done, let's begin with a simple example. The following program uses an anonymous method that counts from 0 to 5.

```
// Demonstrate an anonymous method.
using System;

// Declare a delegate type.
delegate void CountIt();

class AnonMethDemo {
    static void Main() {
        // Here, the code for counting is passed
        // as an anonymous method.
        CountIt count = delegate {
            // This is the block of code passed to the delegate.
            for(int i=0; i <= 5; i++)
                Console.WriteLine(i);
        }; // notice the semicolon
        count();
    }
}
```

This program first declares a delegate type called CountIt that has no parameters and returns void. Inside Main(), a CountIt instance called count is created, and it is passed the block of code that follows the delegate keyword. This block of code is the anonymous method that will be executed when count is called. Notice that the block of code is followed by a semicolon, which terminates the declaration statement. The output from the program is shown here:

```
0
1
2
3
4
5
```