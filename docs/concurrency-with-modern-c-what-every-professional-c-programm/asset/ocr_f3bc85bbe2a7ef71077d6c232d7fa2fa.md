# ## 3.6 Cooperative Interruption (C++20)

The additional functionality of the cooperative interruption thread is based on the std::stop_source, std::stop_token, and the std::stop_callback classes. std::jthread and std::condition_variable_any support cooperative interruption by design.

First, why it is not a good idea to kill a thread?

# ### Killing a Thread is Dangerous

Killing a thread is dangerous because you don't know the state of the thread. Here are two possible malicious outcomes.

+   - The thread is only half-done with its job. Consequently, you don't know the state of its job and, hence, the state of your program. You end with undefined behavior, and all bets are off.
+   - The thread may be in a critical section and having locked a mutex. Killing a thread while it locks a mutex ends with a high probability in a deadlock.

The std::stop_source, std::stop_token, and the std::stop_callback classes allows a thread to asynchronously request an execution to stop or ask if an execution got a stop signal. The std::stop_token can be passed to an operation and afterward be used to actively poll the token for a stop request or to register a callback via std::stop_callback. The stop request is sent by a std::stop_source. This signal affects all associated std::stop_token. The three classes std::stop_source, std::stop_token, and the std::stop_callback share the ownership of an associated stop state.

In the next subsections, I provide more details about cooperative interruption.

# ### 3.6.1 std::stop_source

You can construct a std::stop_source in two ways:

Constructors of std::stop_source

```
```cpp
std::stop_source();
explicit std::stop_source(std::nostopstate_t) noexcept;
```
```

The default constructor (line 1) constructs a std::stop_source with a new stop state. The constructor taking std::nostopstate_t (line 2) constructs an empty std::stop_source without associated stop state.

The component std::stop_source src provides the following member functions for handling stop requests.