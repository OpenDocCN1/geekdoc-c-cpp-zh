```
public static void Main()
{
    ThreadStart t1 = new ThreadStart(ChildThread);
    Console.WriteLine("Creating child thread");
    Thread t2 = new Thread(t1);
    t1.Start();

    //main thread is stopped
    Thread.Sleep(2000);

    //child thread aborted
    Console.WriteLine("Aborting child thread");
    t2.Abort();
    Console.Read();
}
}
}
```

# c, the output is:

Creating child thread

Child Thread started

0

1

Aborting child thread

Exception caught

Exception is not handled