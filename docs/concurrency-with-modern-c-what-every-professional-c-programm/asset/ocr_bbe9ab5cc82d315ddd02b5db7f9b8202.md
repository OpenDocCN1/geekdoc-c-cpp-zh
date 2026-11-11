```
```cpp
28        std::cout << "20/10= " << shaFut.get() << '\n';
29
30    }
31
32};
33
34int main(){
35
36    std::cout << std::boolalpha << '\n';
37
38    // define the promises
39    std::promise<int> divPromise;
40
41    // get the future
42    std::future<int> divResult= divPromise.get_future();
43
44    std::cout << "divResult.valid(): " << divResult.valid() << '\n';
45
46    // calculate the result in a separate thread
47    Div div;
48    std::thread divThread(div, std::move(divPromise), 20, 10);
49
50    std::cout << "divResult.valid(): " << divResult.valid() << '\n';
51
52    std::shared_future<int> sharedResult = divResult.share();
53
54    std::cout << "divResult.valid(): " << divResult.valid() << "\n\n";
55
56    Requestor req;
57    std::thread sharedThread1(req, sharedResult);
58    std::thread sharedThread2(req, sharedResult);
59    std::thread sharedThread3(req, sharedResult);
60    std::thread sharedThread4(req, sharedResult);
61    std::thread sharedThread5(req, sharedResult);
62
63    divThread.join();
64
65    sharedThread1.join();
66    sharedThread2.join();
67    sharedThread3.join();
68    sharedThread4.join();
69    sharedThread5.join();
70
71    std::cout << '\n';
72
```
```