
```c
8 // function main begins program execution
9 int main(void)
10 {
11     puts("Sequential calls to fibonacci(50) and fibonacci(49)");
12
13     // calculate fibonacci value for 50
14     time_t startTime1 = time(NULL);
15     puts("Calculating fibonacci(50)");
16     unsigned long long int result1 = fibonacci(50);
17     time_t endTime1 = time(NULL);
18
19     printf("fibonacci(%u) = %llu\n", 50, result1);
20     printf("Calculation time = %f minutes\n\n",
21     difftime(endTime1, startTime1) / 60.0);
22
23     time_t startTime2 = time(NULL);
24     puts("Calculating fibonacci(49)");
25     unsigned long long int result2 = fibonacci(49);
26     time_t endTime2 = time(NULL);
27
28     printf("fibonacci(%u) = %llu\n", 49, result2);
29     printf("Calculation time = %f minutes\n\n",
30     difftime(endTime2, startTime2) / 60.0);
31
32     printf("Total calculation time = %f minutes\n",
33     difftime(endTime2, startTime1) / 60.0);
34 }
35
36 // Recursively calculates fibonacci numbers
37 unsigned long long int fibonacci(unsigned int n)
38 {
39     // base case
40     if (0 == n || 1 == n) {
41         return n;
42     }
43     else { // recursive step
44         return fibonacci(n - 1) + fibonacci(n - 2);
45     }
46 }
```

### a) 双核 Windows 计算机上的输出

```text
Sequential calls to fibonacci(50) and fibonacci(49)
Calculating fibonacci(50)
fibonacci(50) = 12586269025
Calculation time = 1.366667 minutes

Calculating fibonacci(49)
fibonacci(49) = 7778742049
Calculation time = 0.883333 minutes

Total calculation time = 2.250000 minutes
```

图 E.11 | 斐波那契计算按顺序执行。 (第 2 部分，共 3 部分。)

### b) 单核 Windows 计算机上的输出

```text
Sequential calls to fibonacci(50) and fibonacci(49)
Calculating fibonacci(50)
fibonacci(50) = 12586269025
Calculation time = 1.566667 minutes

Calculating fibonacci(49)
fibonacci(49) = 7778742049
Calculation time = 0.883333 minutes

Total calculation time = 2.450000 minutes
```

### c) 单核 Windows 计算机上的输出

```text
Sequential calls to fibonacci(50) and fibonacci(49)
Calculating fibonacci(50)
fibonacci(50) = 12586269025
Calculation time = 1.450000 minutes

Calculating fibonacci(49)
fibonacci(49) = 7778742049
Calculation time = 0.883333 minutes

Total calculation time = 2.333333 minutes
```

图 E.11 | 斐波那契计算按顺序执行。 (第 3 部分，共 3 部分。)

第一个输出显示了在双核 Windows 计算机上执行程序的结果，在该计算机上每次执行都产生相同的结果，尽管这不能保证。第二个和第三个输出显示了在单核 Windows 计算机上执行程序的结果，在该计算机上结果有所不同，但执行时间总是更长，因为处理器在该程序和同时在计算机上执行的其他所有程序之间共享。

## 示例：两个计算密集型任务的多线程执行

图 E.12 也使用了递归斐波那契函数，但以单独的线程执行对其的每次调用。前两个输出显示了多线程斐波那契示例在双核计算机上的执行。尽管执行时间有所变化，但在我们的测试中，执行两次斐波那契计算的总时间始终少于图 E.11 中的顺序执行——因为我们的程序拆分为两个线程并使用了两个核心，而不是只有一个。后两个输出显示了该示例在与双核计算机速度相同的单核计算机上的执行。同样，每次执行的用时各不相同，但总时间超过了顺序执行，这是由于一个处理器在程序的线程和其他同时在计算机上执行的程序之间共享而产生的开销。

```c
1 // Fig. E.12: fig_E_12.c
2 // Fibonacci calculations performed in separate threads
3 #include <stdio.h>
#include <threads.h>
#include <time.h>

#define NUMBER_OF_THREADS 2

int startFibonacci(void *nPtr);
unsigned long long int fibonacci(unsigned int n);

typedef struct ThreadData {
    time_t startTime; // time thread starts processing
    time_t endTime; // time thread finishes processing
    unsigned int number; // fibonacci number to calculate
} ThreadData; // end struct ThreadData

int main(void)
{
    // data passed to the threads; uses designated initializers
    ThreadData data[NUMBER_OF_THREADS] =
        { [0] = {.number = 50},
          [1] = {.number = 49}};

    // each thread needs a thread identifier of type thrd_t
    thrd_t threads[NUMBER_OF_THREADS];

    puts("Fibonacci(50) and fibonacci(49) in separate threads");

    // create and start the threads
    for (size_t i = 0; i < NUMBER_OF_THREADS; ++i) {
        printf("Starting thread to calculate fibonacci(%d)\n",
               data[i].number);

        // create a thread and check whether creation was successful
        if (thrd_create(&threads[i], startFibonacci, &data[i]) !=
            thrd_success) {
            puts("Failed to create thread");
        }
    }

    // wait for each of the calculations to complete
    for (size_t i = 0; i < NUMBER_OF_THREADS; ++i)
        thrd_join(threads[i], NULL);

    // determine time that first thread started
    time_t startTime = (data[0].startTime < data[1].startTime) ?
        data[0].startTime : data[1].startTime;

    // determine time that last thread terminated
    time_t endTime = (data[0].endTime > data[1].endTime) ?
        data[0].endTime : data[1].endTime;

    // display total time for calculations
    printf("Total calculation time = %f minutes\n", difftime(endTime, startTime) / 60.0);
}

// Called by a thread to begin recursive Fibonacci calculation
int startFibonacci(void *ptr)
{
    // cast ptr to ThreadData * so we can access arguments
    ThreadData *dataPtr = (ThreadData *) ptr;

    dataPtr->startTime = time(NULL); // time before calculation

    printf("Calculating fibonacci(%d)\n", dataPtr->number);
    printf("fibonacci(%d) = %llu\n", dataPtr->number, fibonacci(dataPtr->number));

    dataPtr->endTime = time(NULL); // time after calculation

    printf("Calculation time = %f minutes\n\n", difftime(dataPtr->endTime, dataPtr->startTime) / 60.0);
    return thrd_success;
}

// Recursively calculates fibonacci numbers
unsigned long long int fibonacci(unsigned int n)
{
    // base case
    if (0 == n || 1 == n) {
        return n;
    } else { // recursive step
        return fibonacci(n - 1) + fibonacci(n - 2);
    }
}
```

图 E.12 | 斐波那契计算在单独的线程中执行。 (第 1 部分，共 4 部分。)

### a) 双核 Windows 计算机上的输出

```text
fibonacci(50) and fibonacci(49) in separate threads
Starting thread to calculate fibonacci(50)
Starting thread to calculate fibonacci(49)
Calculating fibonacci(50)
Calculating fibonacci(49)
fibonacci(49) = 7778742049
Calculation time = 0.866667 minutes

fibonacci(50) = 12586269025
Calculation time = 1.466667 minutes

Total calculation time = 1.466667 minutes
```

### b) 双核 Windows 计算机上的输出

```text
fibonacci(50) and fibonacci(49) in separate threads
Starting thread to calculate fibonacci(50)
Starting thread to calculate fibonacci(49)
Calculating fibonacci(50)
Calculating fibonacci(49)
fibonacci(49) = 7778742049
Calculation time = 0.783333 minutes

fibonacci(50) = 12586269025
Calculation time = 1.266667 minutes

Total calculation time = 1.266667 minutes
```

### c) 单核 Windows 计算机上的输出

```text
fibonacci(50) and fibonacci(49) in separate threads
Starting thread to calculate fibonacci(50)
Starting thread to calculate fibonacci(49)
Calculating fibonacci(50)
Calculating fibonacci(49)
fibonacci(49) = 7778742049
Calculation time = 0.683333 minutes

fibonacci(50) = 12586269025
Calculation time = 2.183333 minutes

Total calculation time = 2.183333 minutes
```

### d) 单核 Windows 计算机上的输出

```text
fibonacci(50) and fibonacci(49) in separate threads
Starting thread to calculate fibonacci(50)
Starting thread to calculate fibonacci(49)
Calculating fibonacci(50)
Calculating fibonacci(49)
fibonacci(49) = 7778742049
Calculation time = 1.600000 minutes

fibonacci(50) = 12586269025
Calculation time = 2.083333 minutes

Total calculation time = 2.083333 minutes
```

图 E.12 | 斐波那契计算在单独的线程中执行。 (第 4 部分，共 4 部分。)

## 结构体 ThreadData

此示例中每个线程执行的函数将 ThreadData 对象作为其参数接收。该对象包含将传递给 fibonacci 的数字以及两个 time_t 成员，用于存储每个线程的 fibonacci 调用前后的时间。第 21-23 行创建了两个 ThreadData 对象的数组，并使用指定初始化器将它们的 number 成员分别设置为 50 和 49。
