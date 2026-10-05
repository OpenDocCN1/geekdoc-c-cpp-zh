# C++ Standard Library: std::thread

C++11 implements a threading library through #include <thread>. When a program begins execution, the operating system executes the program in the program's own process space. The basic idea behind threads is to sub-divide a process into a number of independently executing threads. The purpose is to improve the performance of the program by executing multiple threads concurrently.

By default when a C++ program begins execution, it starts in a default thread main. If the program does not create any threads then it runs entirely in the main thread. The program is said to be a single threaded application.

# Basic Thread Creation

The following program uses two threads to compute the number of odd and even numbers in a range:

```
#include <iostream>
#include <thread>

size_t oddsum = 0;
size_t evensum = 0;

void even_sum(int start, int stop) {
    for (int i = start; i < stop; i++)
        if (i%2 == 0 ) evensum += i;
}
void odd_sum(int start, int stop) {
    for (int i = start; i < stop; i++)
        if (i%2 != 0 ) oddsum += i;
}

int main() {
    size_t start = 1000;
    size_t stop = 90678124;

    // create thread objects t1 and t2
    std::thread t1(even_sum, start, stop);
    std::thread t2(odd_sum, start, stop);
```