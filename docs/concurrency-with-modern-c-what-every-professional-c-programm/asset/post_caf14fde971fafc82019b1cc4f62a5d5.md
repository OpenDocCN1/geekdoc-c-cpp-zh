
```cpp
}
```

The program executes two promises in their threads. The resulting futures are fire and forget futures. These futures block in their destructors until the associated promise is done. The result is that the promises are executed in the sequence which you find in the source code. The execution sequence is independent of the execution time. This is what you see in the output of the program.

![](img/d61a6c83410484053b8892275d2fcc4f_211_0.png)

Fire and forget futures

std::async is a convenient mechanism used to distribute a bigger compute job on more shoulders.

### 3.9.2.3 Concurrent Calculation

The calculation of the scalar product can be spread across four asynchronous function calls.

**Dot product with four futures**

```cpp
// dotProductAsync.cpp

#include <iostream>
#include <future>
#include <random>
#include <vector>
#include <numeric>

using namespace std;

static const int NUM = 10000000;

long long getDotProduct(vector<int>& v, vector<int>& w) {

    auto vSize = v.size();

    auto future1 = async([&] {
```

The program uses the functionality of the random library that is part of C++11. The two vectors *v* and *w* are created and filled with random numbers (lines 50 - 56). Each of the vectors gets (lines 53 - 56) one hundred million elements. `dist(engine)` in lines 54 and 55 generates the random numbers, which are uniformly distributed in the range 0 to 100. The calculation of the scalar product takes place in `getDotProduct` (lines 13 - 34). The standard algorithm `std::inner_product` is executed asynchronously four times: one asynchronous invocation for each quarter of the vectors' length. The return statement sums up the results of the futures.

![](img/d61a6c83410484053b8892275d2fcc4f_213_0.png)

`std::packaged_task` is also usually used to perform a concurrent computation.

### 3.9.3 `std::packaged_task`

`std::packaged_task` `pack` is a wrapper for a callable in order to be invoked asynchronously. By calling `pack.get_future()` you get the associated future. Invoking the call operator on `pack` (`pack()`) executes the `std::packaged_task` and, therefore, executes the callable.

Dealing with `std::packaged_task` usually consists of four steps:

- I. Wrap your work:
  ```cpp
  std::packaged_task<int(int, int)> sumTask([](int a, int b){ return a + b; });
  ```
- II. Create a future:
  ```cpp
  std::future<int> sumResult = sumTask.get_future();
  ```
- III. Perform the calculation:
  ```cpp
  sumTask(2000, 11);
  ```
- IV. Query the result:
  ```cpp
  sumResult.get();
  ```

Here is an example showing the four steps.

**Concurrency with std::packaged_task**

```cpp
// packagedTask.cpp

#include <utility>
#include <future>
#include <iostream>
#include <thread>
#include <deque>

class SumUp{
public:
    int operator()(int beg, int end){
        long long int sum{0};
        for (int i = beg; i < end; ++i ) sum += i;
        return sum;
    }
};

int main(){

    std::cout << '\n';

    SumUp sumUp1;
    SumUp sumUp2;
    SumUp sumUp3;
    SumUp sumUp4;

    // wrap the tasks
    std::packaged_task<int(int, int)> sumTask1(sumUp1);
    std::packaged_task<int(int, int)> sumTask2(sumUp2);
    std::packaged_task<int(int, int)> sumTask3(sumUp3);
    std::packaged_task<int(int, int)> sumTask4(sumUp4);

    // create the futures
    std::future<int> sumResult1 = sumTask1.get_future();
    std::future<int> sumResult2 = sumTask2.get_future();
    std::future<int> sumResult3 = sumTask3.get_future();
    std::future<int> sumResult4 = sumTask4.get_future();

    // push the tasks on the container
    std::deque<std::packaged_task<int(int, int)>> allTasks;
    allTasks.push_back(std::move(sumTask1));
    allTasks.push_back(std::move(sumTask2));
    allTasks.push_back(std::move(sumTask3));
    allTasks.push_back(std::move(sumTask4));

    int begin{1};
    int increment{2500};
    int end = begin + increment;

    // perform each calculation in a separate thread
    while (not allTasks.empty()){
        std::packaged_task<int(int, int)> myTask = std::move(allTasks.front());
        allTasks.pop_front();
        std::thread sumThread(std::move(myTask), begin, end);
        begin = end;
        end += increment;
        sumThread.detach();
    }

    // pick up the results
    auto sum = sumResult1.get() + sumResult2.get() +
               sumResult3.get() + sumResult4.get();

    std::cout << "sum of 0 .. 10000 = " << sum << '\n';

    std::cout << '\n';

}
```

The program’s purpose is to calculate the sum of all numbers from 0 to 10000 - with the help of four `std::packaged_task` each running in a separate thread. The associated futures are used, to sum up the final result. Of course, you can use the Gaußschen Summenformel²². Strange, I didn’t find an English web page.

**I. Wrap the tasks:** I pack the work packages in `std::packaged_task` (lines 28 - 31) objects. Work packages are instances of the class SumUp (lines 9 - 16). The work is done in the call operator (lines 11 - 15). The call operator sums up all numbers from beg to end - 1 and returns the sum as a result. `std::packaged_task` in lines 28 - 31 can deal with callables that need two ints and return an `int`: `int(int, int)`.

**II. Create the futures:** I have to create the future objects with the help of `std::packaged_task` objects. This is done in the lines 34 to 37. The packaged_task is the promise in the communication channel. The type of the future is defined explicitly: `std::future<int> sumResult1 = sumTask1.get_future()`, but the compiler can do that job for me: `auto sumResult1 = sumTask1.get_future()`.

> ²² https://de.wikipedia.org/wiki/Gau%C3%9Fsche_Summenformel

**Reuse of a `std::packaged_task`**

```cpp
// packagedTaskReuse.cpp

#include <functional>
#include <future>
#include <iostream>
#include <utility>
#include <vector>

void calcProducts(std::packaged_task<int(int, int)>& task,
                  const std::vector<std::pair<int, int>>& pairs){
    for (auto& pair: pairs){
        auto fut = task.get_future();
        task(pair.first, pair.second);
        std::cout << pair.first << " * " << pair.second << " = " << fut.get()
                  << '\n';
        task.reset();
    }
}

int main(){

    std::cout << '\n';

    std::vector<std::pair<int, int>> allPairs;
    allPairs.push_back(std::make_pair(1, 2));
    allPairs.push_back(std::make_pair(2, 3));
    allPairs.push_back(std::make_pair(3, 4));
    allPairs.push_back(std::make_pair(4, 5));

    std::packaged_task<int(int, int)> task{[](int fir, int sec){
        return fir * sec; }
    };

    calcProducts(task, allPairs);

    std::cout << '\n';

    std::thread t(calcProducts, std::ref(task), allPairs);
    t.join();

    std::cout << '\n';

}
```

The function calcProducts (line 9) gets two arguments: the task and the int-pairs vector. It uses the task to calculate for each int-pair the product (line 13). In the end, the task is reset in line 16. calcProducts runs in the main-thread (line 34) and a separate thread (line 38). Here is the output of the program.

![](img/d61a6c83410484053b8892275d2fcc4f_218_0.png)

Reuse of a std::packaged_task

### 3.9.4 `std::promise` and `std::future`

The class templates std::promise and std::future provide you with full control over the task.
Promise and future are a mighty pair. A promise can put a value, an exception, or simply a notification into the shared data channel. One promise can serve many std::shared_future futures. With C++23 we may get extended futures that are composable.

Here is an introductory example of the usage of std::promise and std::future. Both communication endpoints can be moved to separate threads, so the communication takes place between threads.

**Usage of std::promise and std::future**

```cpp
// promiseFuture.cpp

#include <future>
#include <iostream>
#include <thread>
#include <utility>

void product(std::promise<int>&& intPromise, int a, int b){
  intPromise.set_value(a*b);
```
