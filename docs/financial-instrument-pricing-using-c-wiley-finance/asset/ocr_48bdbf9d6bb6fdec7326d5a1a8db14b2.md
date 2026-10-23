```
bool stop;
std::size_t f;
while ((stop = concurrency::receive(_stop)) == false)
{
    f = concurrency::receive(_mis);
    if (((f/freq)*freq == f))
    {
        std::cout << f << ",";
    }
}

done();
ThreadSafePrint("Exit MIS");
};
```

For completeness, we show the utility function to print text on the console in a thread-safe way:

```
void ThreadSafePrint(const std::string& s)
{ // Function to avoid garbled output on the console

    std::mutex my_mutex;
    std::lock_guard<std::mutex> guard(my_mutex);
    std::cout << s << '\n';
}
```

We now discuss the steps that are needed to configure a Monte Carlo option calculator based on the actor model. The model is based on the design decision that the path evolver delivers data to several pricing agents and it can also send progress information to several management and watchdog systems. We represent these requirements in a UML diagram in Figure 32.4. In other words, this diagram gives insight on how to configure an application. In particular, we note the 1:N multiplicity relationships between the agents. We discuss one example. First, we create message buffers and option-related data:

![](bbox=[0.12, 0.73, 0.88, 0.92])

FIGURE 32.4 UML class diagram (with multiplicities)