```
Parallel.For(0, 1000, doLoopWork);
...
private void doLoopWork(int i, ParallelLoopState p)
{
    if (i > 600)
    {
        p.Stop();
    }
}
```