```
std::vector<int> vecInt = { 1, 2, 0, 2, 3, 3, 1, 3, 2, 2, 1 };
print<int, std::vector>(vecInt, std::string("Before remove (all):"));

int removeIntValue = 1;
std::vector<int>::iterator pos
    = remove(vecInt.begin(), vecInt.end(), removeIntValue);
vecInt.erase(pos, vecInt.end());

print(vecInt, std::string("After remove (all):"));

pos = std::remove_if(vecInt.begin(), vecInt.end(),
                     std::bind2nd(std::greater<int>(), 0));
vecInt.erase(pos, vecInt.end()); // Physical operation
print(vecInt, std::string("After remove (criterion):"));

// Removing duplicates, C arrays
int src[] = { 1, 1, 1, 3, 5, 5, 6, 6, 6 };
std::list<int> myList1;
std::copy(src, src + (sizeof(src) / sizeof(src[0])),
          back_inserter(myList1));

// remove consecutive duplicates
std::list<int>::iterator end = unique(myList1.begin(), myList1.end());
myList1.erase(end, myList1.end()); // Physical MultiplyByTwo
print(myList1, std::string("List without duplicates:"));

// Copying and removing. This is a combination of copy and remove.
double removeValue = 5; // Copy everything that is not this value
v1.clear(); v1 = { 5, 1, 2, 3, 4, 5, 6, 5 };
v2.clear(); v2.resize(v1.size());   // v2 is big enough to hold data.
std::remove_copy(v1.begin(), v1.end(), v2.begin(), removeValue);

// You need to physically replace unwanted elements.
// Remove redundant space

v2.erase(remove(v2.begin(), v2.end(), 0.0), v2.end());

print(v1, "v1 after remove_copy()");
print(v2, "v2 after remove_copy()");

// Replace all values > 3 and put them into v2.
v1.clear(); v1 = { 1, 2, 3, 5, 6, 2, 7 };
v2.clear(); v2.resize(v1.size());
double thresholdValue = 3;
int newValue = 99;
std::remove_copy_if(v1.begin(), v1.end(), v2.begin(),
                    std::bind2nd(std::greater<double>(),
                                thresholdValue));
print(v2, "v2 after remove_copy_if()");

// Removing *consecutive* duplicates. Sequence must be sorted,
// at the least elements with same value are adjacent.
```