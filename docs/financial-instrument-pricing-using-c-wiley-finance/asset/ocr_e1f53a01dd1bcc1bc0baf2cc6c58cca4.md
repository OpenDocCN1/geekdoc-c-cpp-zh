A useful piece of C++ syntax to determine how many processors there are on your system is:

```
// Display the number of processors/cores
std::cout<<std::thread::hardware_concurrency();
```

A discussion of *thread notification* is outside the scope of this chapter.

# 28.2 THREAD FUNDAMENTALS

In C++ the way to create and run threads is to instantiate the class std::thread. It has a number of constructors:

+   - Default constructor (not a thread).
+   - Move constructor.
+   - Creating a thread with a *callable object* as input argument.
+   - (Copy constructor is not supported.)

We create a thread using two stored lambda functions as *thread function* (we shall give more examples of callable objects in Section 28.3). The first function has no input arguments while the second function has two input arguments. The code is:

```
int main()
{
    // Create a thread + thread function
    auto f = []() { std::cout << "Hello world\n"; };
    std::thread t(f);
    // Wait for thread to finish (mandatory)
    t.join();

    // Thread function having input arguments
    auto f2 = [](int n, std::string& s)
        { std::cout << n << " Hello world " << s; };
    std::thread t2(f2, 42, std::string("and beyond\n"));
    // Wait for thread to finish (mandatory)
    t2.join();
}
```

In this case the main thread creates (*forks*) two threads that start executing immediately. The main thread waits for the other threads to complete by calling join() on each one.

It is possible to query some properties of a thread, for example if it is still running, the thread’s ID, getting a POSIX-compliant thread handle and querying the number of concurrent threads supported by the implementation:

```
void ThreadStatus(std::thread& t)
{
    std::cout << "Still running?"<<std::boolalpha
              << t.joinable() << '\n';
    std::cout << "Thread ID:  " << t.get_id() << '\n';
```