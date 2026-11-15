By abstracting the concept of a thread into Task, the .NET multithreading API reduces the complexities of efficiently managing the thread—that is, when to create a new operating system thread and when to reuse an existing one. Similarly, the internal behavior of the Task (via System.Threading.ThreadPool) manages when to return a thread to the thread pool for later reuse and when to deallocate the thread and release any resources it may be consuming.

The work of programming the Task involves assigning the set of instructions the Task will execute and then starting the Task. Not surprisingly, assigning the instructions is heavily dependent on delegates. Listing 18.1 provides a simple example, and Output 18.1 shows a partial listing of the results.

# LISTING 18.1: Starting a Method in a Separate Thread

```
using System;
using System.Threading.Tasks;

public class Program
{
    public static void Main()
    {
        const int repetitions = 10000;
        Task task = new Task(() =>
        {
            for (int count = 0; count < repetitions; count++)
                Console.Write('-');
        });

        task.Start();
        for (int count = 0; count < repetitions; count++)
        {
            Console.Write('.');
        }

        // Wait until the Task completes
        task.Wait();
    }
}
```