```
4 #include <threads.h>
5 #include <time.h>
6
7 #define NUMBER_OF_THREADS 2
8
9 int startFibonacci(void *nPtr);
10 unsigned long long int fibonacci(unsigned int n);
11
12 typedef struct ThreadData {
13     time_t startTime; // time thread starts processing
14     time_t endTime; // time thread finishes processing
15     unsigned int number; // fibonacci number to calculate
16 } ThreadData; // end struct ThreadData
17
18 int main(void)
19 {
20     // data passed to the threads; uses designated initializers
21     ThreadData data[NUMBER_OF_THREADS] =
22         { [0] = {.number = 50},
23         [1] = {.number = 49}};
24
25     // each thread needs a thread identifier of type thrd_t
26     thrd_t threads[NUMBER_OF_THREADS];
27
28     puts("fibonacci(50) and fibonacci(49) in separate threads");
29
30     // create and start the threads
31     for (size_t i = 0; i < NUMBER_OF_THREADS; ++i) {
32         printf("Starting thread to calculate fibonacci(%d)\n",
33             data[i].number);
34
35         // create a thread and check whether creation was successful
36         if (thrd_create(&threads[i], startFibonacci, &data[i]) !=
37             thrd_success) {
38
39         puts("Failed to create thread");
40         }
41     }
42
43     // wait for each of the calculations to complete
44     for (size_t i = 0; i < NUMBER_OF_THREADS; ++i)
45         thrd_join(threads[i], NULL);
46
47     // determine time that first thread started
48     time_t startTime = (data[0].startTime < data[1].startTime) ?
49         data[0].startTime : data[1].startTime;
50
51     // determine time that last thread terminated
52     time_t endTime = (data[0].endTime > data[1].endTime) ?
53         data[0].endTime : data[1].endTime;
```