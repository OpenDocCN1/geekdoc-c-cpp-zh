```
```cpp
#include <chrono> // time measurement
using std::map; using std::cout; using std::endl; using namespace std::chrono;
struct Node {
    std::unique_ptr<int> d_;
    Node() : Node(0) { }
    explicit Node(int d) : d_{ new int } { *d_ = d; }   // also some memory
    friend bool operator<(const Node& a, const Node& b) { return *a.d_<*b.d_; }
    friend bool operator==(const Node& a, const Node& b) { return *a.d_==*b.d_; }
};
long long millisSince(steady_clock::time_point start) { // Helper for measurement
    return duration_cast<milliseconds>(steady_clock::now()-start).count();
}

int main() {
    std::unique_ptr<map<int,Node>> huge{ new map<int,Node>{} };
    cout << "Building..." << endl;
    steady_clock::time_point start = steady_clock::now();
    for(int idx=0; idx < 100*1000*1000; ++idx) { // massive amount in the map
        (*huge)[idx] = Node{idx};
    }
    cout << "Done: " << millisSince(start) << " ms" << endl; // timing here
    start = steady_clock::now();
    huge.reset();                                           // cleanup here
    cout << "End: " << millisSince(start) << " ms" << endl; // timing here
}
```
```

# Listing 20.16 Is it worth saving the release of memory?

To measure how long something takes after exiting main(), you would need timing outside the program. Here, I simulate the cleanup of the map by calling huge.reset(), telling unique_ptr to clean up its charge. You would have done the same without smart pointers with the following:

```
```cpp
map<int,Node>* huge = new map<int,Node>{};
// ...
delete huge;
```
```

But here you want to avoid raw pointers. In both cases, the rule is this: If you omit delete huge; or write huge.release(); instead of reset(), you save the time needed to clean up the many Node objects. You can find out how much time you save at "End:".

At "Done:", millisSince determines the time in milliseconds required to build the data structure. I chose the number 100*1000*1000 (i.e., 100 million) so that my computer can just handle it: