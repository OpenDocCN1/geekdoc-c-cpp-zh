```
// The task is created and it is set up with the correct
properties – these will be
    // our parameters.
    tasks[index] = new GenerateNumbersTask()
    {
        Numbers = numbers,
        Count = 1000,
        StartIndex = index * 1000
    };

    // Create the thread
    threads[index] = new
Thread(tasks[index].GenerateNumbers);

    // Start the thread running
    threads[index].Start();
}

// Wait and then join up with each of the threads in turn so
that
    // when we move on, we know that all of the work has been
done.
    for (int index = 0; index < threadCount; index++)
    {
        threads[index].Join();
    }
}
```