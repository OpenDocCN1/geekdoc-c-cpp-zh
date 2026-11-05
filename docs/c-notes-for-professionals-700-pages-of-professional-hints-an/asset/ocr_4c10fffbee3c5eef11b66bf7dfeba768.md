```
Thread.Sleep(100);
lock (resourceA)
{
    Thread.Sleep(100);
    lock (resourceB)
    {
        output += "T1#";
    }
}
}

public void Thread2DoWork()
{
    Thread.Sleep(100);
    lock (resourceB)
    {
        Thread.Sleep(100);
        lock (resourceA)
        {
            output += "T2#";
        }
    }
}
}
```

To avoid being deadlocked this way, one can use Monitor.TryEnter(lock_object, timeout_in_milliseconds) to check if a lock is held on an object already. If Monitor.TryEnter does not succeed in acquiring a lock on lock_object before timeout_in_milliseconds, it returns false, giving the thread a chance to release other held resources and yielding, thus giving other threads a chance to complete as in this slightly modified version of the above:

```
private void button_Click(object sender, EventArgs e)
{
    MonitorWorkers workers = new MonitorWorkers();
    workers.StartThreads();
    textBox.Text = workers.GetResult();
}

private class MonitorWorkers
{
    Thread thread1, thread2;

    object resourceA = new object();
    object resourceB = new object();

    string output;

    public void StartThreads()
    {
        thread1 = new Thread(Thread1DoWork);
        thread2 = new Thread(Thread2DoWork);
        thread1.Start();
        thread2.Start();
    }

    public string GetResult()
    {
        thread1.Join();
        thread2.Join();
        return output;
    }
}
```