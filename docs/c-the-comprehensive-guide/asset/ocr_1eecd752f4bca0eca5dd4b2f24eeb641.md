```
```cpp
void task1() { auto r = fib(40); cout << "fib(40)=" << r << endl; }

void main_program() {
    try {
        std::thread th{ &task1 };
        std::vector data{ 0,1,2 };
        data.at(666);                    // ⚡ triggers out_of_range
        th.join();                       // would wait
    } catch(std::runtime_error &ex) {    // ⚡ does not match out_of_range
        //...
    }
}

int main() {
    try {
        main_program();
    } catch( ... ) {                     // so far, so good, looks safe
        std::cout << "An error has occurred\n"; // you won't see this
    }
}
```
```

In the absence of threads, this would be working code. data.at(666) does throw an exception, but that's not forbidden. The thrown out_of_range exception does not match the runtime_error specified in catch. So the exception leaves main_program and is caught in catch(...). There—without threads—the output “An error ...” would appear. Not so with a still running thread: th is still active at the time of the exception. For exception handling, its block is exited and the destructor of thread is called. And that then leads to terminate(), the immediate program termination.

What if you had already caught everything possible with catch(...) instead of catch(std::runtime_error ex) in the main program? Unfortunately, there’s no difference: the scope of th is still exited when handling the exception in catch. You need to ensure that th still exists within catch—for example, like this.

```
```cpp
// https://godbolt.org/z/T4cGjnY4
#include <iostream>
#include <thread>
#include <vector>
#include <exception>
using std::cout; using std::endl;

long fib(long n) { return n<=1 ? n : fib(n-1)+fib(n-2); }
void task1() { auto r = fib(40); cout << "fib(40)=" << r << endl; }
```
```