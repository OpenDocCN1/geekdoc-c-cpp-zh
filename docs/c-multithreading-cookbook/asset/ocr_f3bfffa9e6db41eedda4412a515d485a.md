```
{
  params->this_ptr->Min() = dMin;
}
params->this_ptr->Score() = dScore;
if (dBest < params->this_ptr->Best()) {
    params->this_ptr->Best() = dBest;
}
```

ReleaseMutex(hMutex);
CloseHandle(hMutex);

return 0;

Now, as you can see, we have designed statements in such a manner that all the accesses to the shared memory locations are protected. The references to the shared objects are remove the loop using shared objects and protecting access for them inside the loop won't do much good! Code like that would only slow the application down because we would lose concurrency if the majority protected. That's why we add shared storage so that the calculations are made in parallel. In the beginning of the thread, we have to protect the statements where we read the shared objects, then we'll use the thread-local variables, and at the end, we will again protect the shared objects and we'll then perform the write operations. Safe and clean!

# There's more...

When we think about how to improve the application's performance, we can consider using parallelism to achieve the same, but we must always take care of two things: the performance speed-up and the efficiency. Both things matter when we compare the performances of the sequential algorithm to the parallel one.

In practice, there are always situations where your application could be fine-tuned for a specific demand of an important client. For such demands, a carefully-chosen decision of whether or not to use parallelism is very important. If performance improvement will occur, then you should create a strong sequential algorithm and then transform it into parallel. All the time you must about side-effects such as shared objects or access contention.

These situations are like a balance beam (see-saw). If you want to get the leverage on one side, for example, you want to improve the application performance, then you will lose the leverage on the other side. You could use the parallel approach with more work. However, if you do it right, your application will benefit. This exact type of synchronization must be included from the beginning.