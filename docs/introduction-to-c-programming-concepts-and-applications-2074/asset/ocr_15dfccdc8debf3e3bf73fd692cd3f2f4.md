# // QUIZ ANSWERS

1 a To declare a map, you need to first write #include<map>. The declaration needs to specify 2 types in the template: the type of the key (a string, in this case) and the type of the value (an integer, in this case). Then, the declaration would be:

```
map<string, int> account;
```

b To access an element of the map, use the [] operator, giving the key inside the []. That will return the appropriate value—in this case, the integer account.

```
account[s]
```

2 Here is one option:

```
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;

int main() {
    vector<pair<string, string>> names;
    string firstname, lastname;
    cout << "Enter names (first, then last), or enter \"done\" when finished." << endl;
```

```
cin >> firstname;
while(firstname != "done") {
    cin >> lastname;
    names.push_back(make_pair(lastname,firstname));
    cin >> firstname;
}
sort(names.begin(), names.end());
for (auto p : names) {
    cout << p.second << " " << p.first << endl;
}
```

Notice first that you have a container of pairs. Each name will be stored as a pair (last name and then first name). You will store these in a vector. The first loop just reads in first and last names, forms pairs of them, and adds them to the vector. Then, you use the sort algorithm to sort the vector. This will sort the pairs from smallest to largest; that is, it will sort the names from first alphabetically (by last name) to last alphabetically. If the last name (the first element of the pair) is the same, then it will compare first names (the second element of the pair). Finally, you use an iterator to go through the names and print them out in order.

3 a 2. The find algorithm uses a linear search over a (possibly unordered) container.

b 6. Tuples group arbitrary numbers of elements but can result in awkward code.

c 4. Maps are the way of letting you look up a value for a given key.

d 3. The lower_bound algorithm can only be used after the container is sorted.

e 7. Priority queues have elements pushed in any order, but the top element is the largest one.

f 1. Sorting is often used to make subsequent operations more efficient.

g 5. The pair groups 2 elements, which are accessed through the first and second members.