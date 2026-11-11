duration as an argument.

![](bbox=[0.109, 0.133, 0.177, 0.173])

# ## Access to the system-specific implementation

The threading interface is a wrapper around the underlying implementation. You can use the member function `native_handle` to get access to the system-specific implementation. This handle to the underlying implementation is available for threads, mutexes, and condition variables.

Threads cannot be copied but can be moved. The swap member function performs a move when possible.

To conclude this subsection, here are a few of the mentioned member functions in practice.

# ### Member functions of a thread

```
~~~cpp
// threadMethods.cpp

#include <iostream>
#include <thread>

using namespace std;

int main(){

  cout << boolalpha << '\n';

  cout << "hardware_concurrency()= " << thread::hardware_concurrency() << '\n';

  thread t1([]{cout << "t1 with id= " << this_thread::get_id() << '\n';});
  thread t2([]{cout << "t2 with id= " << this_thread::get_id() << '\n';});

  cout << '\n';

  cout << "FROM MAIN: id of t1 " << t1.get_id() << '\n';
  cout << "FROM MAIN: id of t2 " << t2.get_id() << '\n';

  cout << '\n';
  swap(t1,t2);

  cout << "FROM MAIN: id of t1 " << t1.get_id() << '\n';
  cout << "FROM MAIN: id of t2 " << t2.get_id() << '\n';

  cout << '\n';
}
~~~
```