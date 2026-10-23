```
```cpp
{
    threadGroup.emplace_back(std::shared_ptr<std::thread>
        (new std::thread(tGroupFunctions[i])));
}

for (std::size_t i = 0; i < tGroupFunctions.size(); ++i)
{
    if (threadGroup[i]->joinable())
    {
        threadGroup[i]->join();
    }
}
```
```

*Boost.Thread* contains the class `thread_group` that supports the creation and management of a group of threads as one entity. The threads in the group are related in some way. The functionality is:

+   - Create a new thread group with no threads.
+   - Delete all threads in the group.
+   - Create a new thread and add it to the group.
+   - Remove a thread from the group without deleting the thread.
+   - `join_all()`: call `join()` on each thread in the group.
+   - `size()`: give the number of threads in the group.

The corresponding code (using the variables from Section 32.2.3) is:

```
```cpp
boost::thread_group threads;
for (std::size_t i = 0; i < tGroupFunctions.size(); ++i)
{
    threads.create_thread(tGroupFunctions[i]);
}
std::cout << "Thread group size: " << threads.size() << '\n';

threads.join_all();
```
```

It is possible to create your own class that emulates Boost thread groups if you prefer not to use Boost libraries for this problem.

# 32.3  A FAMILY OF PREDICTOR–CORRECTOR SCHEMES

We now discuss a scheme to be used for one-factor and multifactor SDEs. It is called the *predictor–corrector* method and is a generalisation of a similar scheme that is used to solve ordinary differential equations (Lambert, 1991). In order to apply it to SDEs we examine the nonlinear problem given by equation (31.7). If we discretise this SDE using the trapezoidal