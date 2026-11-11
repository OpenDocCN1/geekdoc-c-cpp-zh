```
~~~cpp
18
19        std::cout << '\n';
20
21        std::jthread thr1 = std::jthread(func);
22        std::jthread thr2 = std::jthread(func);
23        thr1.request_stop();
24        thr2.request_stop();
25
26        std::cout << '\n';
27
28 }
~~~
```

![](bbox=[0.28, 0.36, 0.72, 0.56])

Stop request arrives before the callback registration

The previous program `invokeCallbacks.cpp` illustrates when the stop request arrives before the callback registration, and thus the child thread has to execute each handler during registration.

The following program, `invokeCallbacksLoop.cpp`, illustrates when the callback has been registered before the stop request.

# ### Stop request arrives after the callback registration

```
~~~cpp
1 // invokeCallbacksLoop.cpp
2
3 #include <chrono>
4 #include <functional>
5 #include <iostream>
6 #include <list>
7 #include <stop_token>
8 #include <thread>
9
10 using namespace std::literals;
11
~~~
```