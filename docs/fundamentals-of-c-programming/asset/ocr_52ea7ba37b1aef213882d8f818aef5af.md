```
// Add some names in random order
m["fred"] = um["fred"] = 23;
m["adam"] = um["adam"] = 99;
m["cathy"] = um["cathy"] = 2;
m["wilma"] = um["wilma"] = 50;
m["betty"] = um["betty"] = 19;
m["roger"] = um["roger"] = 44;
m["kim"] = um["kim"] = 7;
m["doug"] = um["doug"] = 10;
m["zach"] = um["zach"] = 5;
m["tom"] = um["tom"] = 34;

// Print the names in each container
for (auto& p : m) {
    std::cout << p.first << ": " << p.second << " ";
    std::cout << '\n';
    std::cout << "----------------------------------\n";
}
for (auto& p : um) {
    std::cout << p.first << ": " << p.second << " ";
    std::cout << '\n';
    std::cout << "----------------------------------\n";
}

// Add some more names to each container
m["tammy"] = um["tammy"] = 80;
m["joey"] = um["joey"] = 80;
m["abby"] = um["abby"] = 80;

// Again, print the names in each container
for (auto& p : m) {
    std::cout << p.first << ": " << p.second << " ";
    std::cout << '\n';
    std::cout << "----------------------------------\n";
}
for (auto& p : um) {
    std::cout << p.first << ": " << p.second << " ";
    std::cout << '\n';
}
}
```

A run of Listing 21.13 (ordvsunord.cpp) on one system prints

![](bbox=[0.185, 0.67, 0.86, 0.83])

The output shows that we can iterate over the elements of a map object in the order of their keys. String keys are ordered lexicographically. The ordering of the unordered map appears random.

Listing 21.13 (ordvsunord.cpp) adds a few additional elements to both map objects. The insertions do