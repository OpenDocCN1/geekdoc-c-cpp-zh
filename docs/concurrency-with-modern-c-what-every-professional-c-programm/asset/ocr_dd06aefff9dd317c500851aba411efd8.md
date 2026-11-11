```
```cpp
39 }
40 const auto end= steady_clock::now();
41 lock_guard<mutex> lockOut(coutMutex);
42 cout << this_thread::get_id() << "  waiting time: "
43      << getDifference(start,end) << " ms" << '\n';
44 }
45
46 void consumePeriodically(shared_future<int> fut){
47 const auto start = steady_clock::now();
48 future_status status;
49 do {
50     this_thread::sleep_for(milliseconds(700));
51     status = fut.wait_for(seconds(0));
52     if (status == future_status::timeout) {
53         lock_guard<mutex> lockOut(coutMutex);
54         cout << "     " << this_thread::get_id()
55              << " still waiting." << '\n';
56     }
57     if (status == future_status::ready) {
58         lock_guard<mutex> lockOut(coutMutex);
59         cout << "     " << this_thread::get_id()
60              << " waiting done => Result: " << fut.get() << '\n';
61     }
62 } while (status != future_status::ready);
63 const auto end= steady_clock::now();
64 lock_guard<mutex> lockOut(coutMutex);
65 cout << "     " << this_thread::get_id() << " waiting time: "
66      << getDifference(start,end) << " ms" << '\n';
67 }
68
69 void consumeWithBackoff(shared_future<int> fut){
70 const auto start = steady_clock::now();
71 future_status status;
72 auto dur= milliseconds(1);
73 do {
74     this_thread::sleep_for(dur);
75     status = fut.wait_for(seconds(0));
76     dur *= 2;
77     if (status == future_status::timeout) {
78         lock_guard<mutex> lockOut(coutMutex);
79         cout << "     " << this_thread::get_id()
80              << " still waiting." << '\n';
81     }
82     if (status == future_status::ready) {
83         lock_guard<mutex> lockOut(coutMutex);
```
```