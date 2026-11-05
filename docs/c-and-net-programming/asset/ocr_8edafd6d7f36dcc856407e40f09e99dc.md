```
}
}
}
public class ThreadCreation {
    public static void Main() {
        Console.WriteLine("Before thread start");
        MyThread thr1 = new MyThread();
        MyThread thr2 = new MyThread();
        Thread td1 = new Thread(new ThreadStart(thr1.ThreadTask));
        Thread td2 = new Thread(new ThreadStart(thr2.ThreadTask));
        td1.name = "Thread 1";
        td2.name = "Thread 2";
        tid1.Start();
        tid2.Start();
    }
}
```

# Output

Before thread start
Thread 1
Data 1
Data 2
Thread 2
Data 1
Data 2
Thread 1
Data 3
Data 4
Thread 2
Data 3
Data 4
Thread 1
Data 5
Thread 2
Data 5