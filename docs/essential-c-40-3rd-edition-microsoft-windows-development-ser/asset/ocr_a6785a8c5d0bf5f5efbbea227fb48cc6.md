```
// Increment
for (int i = 0; i < _Total; i++)
{
    _Count++;
}

    task.Wait();
    Console.WriteLine("Count = {0}", _Count);
}

static void Decrement()
{
    // Decrement
    for (int i = 0; i < _Total; i++)
    {
        _Count--;
    }
}
}
```

One possible result of Listing 19.1 appears in Output 19.1.

# OUTPUT 19.1:

```
Count = 113449949
```

The important thing to note about Listing 19.1 is that the output is not 0. It would have been if Decrement() was called directly (sequentially). However, when calling Decrement() asynchronously, a race condition occurs because the individual steps within _Count++ and _Count-- statements intermingle. (As discussed in the Thread Basics Beginner Topic early in Chapter 18, a single statement in C# will likely involve multiple steps.) Consider the sample execution in Table 19.1.

Table 19.1 shows a parallel execution (or a thread context switch) by the transition of instructions appearing from one column to the other. The value of _Count after a particular line has completed appears in the last column. In this sample execution, _Count++ executes twice and _Count-- occurs once. However, the resultant _Count value is 0, not 1. Copying a result back to _Count essentially wipes out any _Count value changes that occurred since the read of _Count on the same thread.