```
```cpp
54        middle = (low + high + 1) / 2; // recalculate the middle
55    } while ((low <= high) && (location == -1));
56
57    return location; // return location of key
58
59 }
60
61 int main() {
62    // use the default random-number generation engine to produce
63    // uniformly distributed pseudorandom int values from 10 to 99
64    std::random_device rd; // used to seed the default_random_engine
65    std::default_random_engine engine{rd()}; // rd() produces a seed
66    std::uniform_int_distribution<int> randomInt{10, 99};
67
68    std::array<int, 15> arrayToSearch; // create 15-element array
69
70    // fill arrayToSearch with random values
71    for (int& item : arrayToSearch) {
72        item = randomInt(engine);
73    }
74
75    std::sort(arrayToSearch.begin(), arrayToSearch.end());
76
77    // display arrayToSearch's values
78    displayElements(arrayToSearch, 0, arrayToSearch.size() - 1);
79
80    // get input from user
81    std::cout << "\nPlease enter an integer value (-1 to quit): ";
82    int searchKey; // value to locate
83    std::cin >> searchKey; // read an int from user
84    std::cout << "\n";
85
86    // repeatedly input an integer; -1 terminates the program
87    while (searchKey != -1) {
88        // use binary search to try to find integer
89        int position{binarySearch(arrayToSearch, searchKey)};
90
91        // return value of -1 indicates integer was not found
92        if (position == -1) {
93            std::cout << std::format("{} was not found.\n", searchKey);
94        }
95        else {
96            std::cout << std::format("{} was found in position {}.\n",
97                searchKey, position);
98        }
99
100        // get input from user
101        std::cout << "\n\nPlease enter an integer value (-1 to quit): ";
102        std::cin >> searchKey; // read an int from user
103        std::cout << "\n";
104    }
105 }
```
```

Fig. 21.2 | Binary Search of an array. (Part 2 of 3.)