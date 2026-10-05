![](bbox=[0.198, 0.068, 0.631, 0.269])

11. Double-click the selected process in the list of processes, click the **Threads** tab, and click the **Start Address** column. You should see something similar to the following screenshot. *Ndll.dll*'s entry point, TppWorkerThread.* (*Tpp stands for thread pool private.).

![](bbox=[0.198, 0.371, 0.631, 0.693])

If you look at other worker threads, you'll see some are waiting for objects such as events. A process can have multiple thread pools, and each thread pool can have a variety of threads doing unrelated tasks. It's up to the developer to assign work and call the thread-pool APIs to register this work through Ndll.dll.

# # Conclusion

This chapter examined the structure of threads, how they are created and managed, and how Windows decides which threads should run, for how long, and on which process or processors. In the next chapter, you'll look at one of the most important aspects of any OS: memory management.