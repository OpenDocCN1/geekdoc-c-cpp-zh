```
std::unique_ptr<int> d;
Node() : Node{0} : d{new int}{*d = d}; // allow some
explicit Node(int d) : d{new int}{*d = d};
memory
friend bool operator<(const Node& a, const Node& b) { return
*a.d<b.d;}
friend bool operator==(const Node& a, const Node& b) { return
*a.d==b.d;}
}
long milliSince(steady_clock::time_point start) { // Helper for
measurement
    return duration<milliseconds>(steady_clock::now()-start).count();
}

int main() {
    std::unique_ptr<std::map<int,Node>> huge = new map<int,Node>();
    cout << "Building..." << endl;
    steady_clock::time_point start = steady_clock::now();
    for(int idx=0; idx < 100*100*1000; ++idx) { // massive amount in the
        map
        huge[idx] = Node();
    }
    cout << ": " << milliSince(start) << " ms" << endl; // timing here
    start = steady_clock::now();
    huge.reset(); // cleanup
    cout << "End: " << milliSince(start) << " ms" << endl; // timing here
}
```

# **Listing 20.16** Is it worth saving the release of memory?

To measure how long something takes after exiting main(), you would need timing outside the program. Here, I simulate the cleanup of the map by telling unique_ptr to clean up its charge. You would have done the same without smart pointers with the following:

```
map<int,Node>> *huge = new map<int,Node>();
//
/-
delete huge;
```