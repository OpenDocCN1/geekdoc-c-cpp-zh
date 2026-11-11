```
```cpp
84         cout << "        " << this_thread::get_id()
85              << " waiting done => Result: " << fut.get() << '\n';
86     }
87 } while (status != future_status::ready);
88 const auto end= steady_clock::now();
89 lock_guard<mutex> lockOut(coutMutex);
90 cout << "        " << this_thread::get_id()
91      << " waiting time: " << getDifference(start,end) << " ms" << '\n';
92 }
93
94 int main(){
95
96     cout << '\n';
97
98     promise<int> prom;
99     shared_future<int> future= prom.get_future();
100    thread producerThread(producer, move(prom));
101
102    thread consumerThread1(consumer, future, seconds(4));
103    thread consumerThread2(consumer, future, seconds(20));
104    thread consumerThread3(consumePeriodically, future);
105    thread consumerThread4(consumeWithBackoff, future);
106
107    consumerThread1.join();
108    consumerThread2.join();
109    consumerThread3.join();
110    consumerThread4.join();
111    producerThread.join();
112
113    cout << '\n';
114
115 }
```
```

I create the promise in the main function (line 98), use the promise to create the associated future (line 99), and move the promise into a separate thread (line 100). I have to move the promise into the thread because it does not support the copy semantic. That is not necessary for the shared futures (lines 102 - 105); they support the copy semantic and can hence be copied.

Before I talk about the thread's work package, let me say a few words about the auxiliary function getDifference (lines 14 - 19). The function takes two time points and returns the time duration between this two timepoints in milliseconds. I use the function a few times.

What about the five created threads?

+   - producerThread: executes the function producer (lines 21 - 25) and publishes its result 2011 after 5 seconds of sleep. This is the result the futures are waiting for.