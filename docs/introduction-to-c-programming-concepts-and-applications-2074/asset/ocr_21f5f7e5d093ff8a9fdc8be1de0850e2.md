# Exercise 1 Solution

Here’s a solution.

```
// Program 23_7
// Map example - dictionary
#include<iostream>
#include<string>
#include<map>
using namespace std;

int main() {
    map<string, string> dictionary;
    dictionary["rock"] = "An object that breaks scissors";
    dictionary["paper"] = "An object that covers rocks";
    dictionary["scissors"] = "An object that cuts paper";

    for (auto& iter : dictionary) {
        cout << iter.first << ": " << iter.second << endl;
    }
}
```

Notice that when you run this, all the dictionary elements are there, but they appear in a different order than the order they were assigned—specifically, they’re iterated through in alphabetical order. This is because you’ve used a map. If you took this same exact code and replaced map with unordered_map, you’d still get the elements printed, but they could be in a random order.

Click here to go back to the exercise.

# READINGS

a Stroustrup, *Programming Principles and Practice Using C++*, chap. 20.

b Lippman, Lajoie, and Moo, *C++ Primer*, sections 3.4 and 9.1–9.3.

# Exercise 2 Solution

Here’s one solution.

```
// Program 23_13
// Sorting Pairs
#include<iostream>
#include<vector>
#include<string>
#include<algorithm>
using namespace std;

int main() {
    vector<pair<double, string> > salaries;
    cout << "Enter a person's name and salary, one name and then one salary per line." << endl;
    cout << "Enter a negative salary to stop." << endl;
    string personname;
    double sal;
    cin >> personname >> sal;
    while (sal >= 0.0) {
        salaries.push_back(make_pair(sal, personname));
        cin >> personname >> sal;
    }
    sort(salaries.begin(), salaries.end());
    for (auto& iter : salaries) {
        cout << iter.first << " " << iter.second << endl;
    }
}
```

Click here to go back to the exercise.