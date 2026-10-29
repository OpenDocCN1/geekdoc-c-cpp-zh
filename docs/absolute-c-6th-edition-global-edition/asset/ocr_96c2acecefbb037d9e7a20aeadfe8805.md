end of the string. Note that by default, end_iterator is initialized to an ending condition that we can use for cur_iterator.

```
string text = "Call me at my desk phone (907) 867-5309 " +
    "or my cell phone 907-350-3491.";
string pattern = R"(\(?\d{3}\)?[\-\s]?\d{3}[-\|\s]\d{4})";
regex reg(pattern);

sregex_iterator cur_iterator(text.begin(), text.end(), reg);
sregex_iterator end_iterator;

while (cur_iterator != end_iterator)
{
    cout << cur_iterator->str() << endl;
    cur_iterator++;
}
```

Sample Dialogue:
(907) 867-5309
907-350-3491

# Threads

A thread is a separate computation process. In C++, you can have programs with multiple threads. You can think of the threads as computations that execute in parallel. On a computer that has enough processors, the threads might indeed execute in parallel. In many computing situations the threads do not really execute in parallel. Instead, the computer switches resources between threads so that each thread in turn does a little bit of computing. To the user this looks like the processes are executing in parallel.

You have already experienced threads. Modern operating systems allow you to run more than one program at the same time. For example, rather than waiting for your virus scanning program to finish its computation, you can go on to, say, read your e-mail while the virus scanning program is still executing. The operating system is using threads to make this happen. There may or may not be some work being done in parallel depending on your computer and operating system. Most likely, the two computation threads are simply sharing computer resources so that they take turns using the computer's resources. When reading your e-mail, you may or may not notice that response is slower because resources are being shared with the virus scanning program. Your e-mail reading program is indeed slowed down, but since humans are so much slower than computers, any apparent slowdown is likely to be unnoticed.

Threads are useful when you need extra speed and want to run computations (possibly) in parallel, and also when you want some processing to continue when another part is blocked/ stopped (perhaps waiting for input). In Graphical Processor Unit (GPU) programming you can have hundreds of thousands of threads! It is possible to run what used to be the equivalent of a supercomputer on a GPU-enabled server or workstation.

As in the rest of this appendix, we provide only an introduction to threads through some examples. The first example shows how to run a function in a separate thread: