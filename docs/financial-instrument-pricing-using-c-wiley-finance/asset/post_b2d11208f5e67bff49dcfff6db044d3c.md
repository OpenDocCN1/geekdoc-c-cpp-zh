
```
double thresholdValue = 3;
newValue = 99;
std::replace_copy_if(v1.begin(), v1.end(), v2.begin(),
                    std::bind2nd(std::greater<double>(),
                    thresholdValue), newValue);
print(v2, "v2 after replace_copy_if()");
}
```

The output is:

```
**** Block V, Replacing ranges ****
After replace (all):: D, D, D, D, D, D, D, D, D, D,
Modified character array:: D, X, D, X, D, D, D, D, D, D,
After replace and predicate:: D, Z, D, Z, D, D, D, D, D, D,
v1 after replace_copy(): 5, 1, 2, 3, 4, 5, 6, 5,
v2 after replace_copy(): 4, 1, 2, 3, 4, 4, 6, 4,
v2 after replace_copy_if(): 1, 2, 3, 99, 99, 2, 99,
```

```
**** Block VI, Removing elements ****
Before remove (all):: 1, 2, 0, 2, 3, 3, 1, 3, 2, 2, 1,
After remove (all):: 2, 0, 2, 3, 3, 3, 2, 2,
After remove (criterion):: 0,
List without duplicates:: 1, 3, 5, 6,
v1 after remove_copy(): 5, 1, 2, 3, 4, 5, 6, 5,
v2 after remove_copy(): 1, 2, 3, 4, 6,
v2 after remove_copy_if(): 1, 2, 3, 2, 0, 0, 0,
unique elements: 1, 2, 3, 4, 1,
remove elements with previous greater element: 2, 13, 16,
unique elements with copy: 2, 13, 4, 16, 7,
Fixed-size arrays
```

## 17.4.5 Removing Elements

*Removing algorithms* are special modifying algorithms. They can remove the elements in a single range or they can remove the elements while they are being copied into another range. The main algorithms are:

- Remove elements with a given value or elements that match/do not match a given criterion.
- Remove adjacent duplicates.
- Copy elements while removing adjacent duplicates.

Some sample code is:

```
void Remove()
{
    // V. Remove algorithms
    // Removing elements from a range or based on a criterion
    std::cout << "\n**** Block VI, Removing elements ****\n";
    std::vector<double> v1 = { 1.0, 2.0, 3.0, 4.0 };
    std::vector<double> v2;
```

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

```
v1.clear(); v1 = { 1, 2, 2, 3, 3, 3, 4, 4, 4, 4, 1 };
v1.erase(std::unique(v1.begin(), v1.end()), v1.end());
print(v1, "unique elements");

// Remove elements if there was a previous greater element.
v1.clear(); v1 = { 2, 13, 4, 16, 7 };
v1.erase(unique(v1.begin(), v1.end(), std::greater<int>()), v1.end());
print(v1, "remove elements with previous greater element");

// Remove duplicates while copying.
v1.clear(); v1 = { 2, 2, 13, 13, 4, 16, 7, 7 };
v2.clear(); v2.resize(v1.size());
v2.erase(std::unique_copy(v1.begin(), v1.end(), v2.begin()), v2.end());
print(v2, "unique elements with copy");
}
```

The output is:

```
**** Block VI, Removing elements ****
Before remove (all):: 1, 2, 0, 2, 3, 3, 1, 3, 2, 2, 1,
After remove (all):: 2, 0, 2, 3, 3, 3, 2, 2,
After remove (criterion):: 0,
List without duplicates:: 1, 3, 5, 6,
v1 after remove_copy(): 5, 1, 2, 3, 4, 5, 6, 5,
v2 after remove_copy(): 1, 2, 3, 4, 6,
v2 after remove_copy_if(): 1, 2, 3, 2, 0, 0, 0,
unique elements: 1, 2, 3, 4, 1,
remove elements with previous greater element: 2, 13, 16,
unique elements with copy: 2, 13, 4, 16, 7,
Fixed-size arrays
```

## 17.5 COMPILE-TIME ARRAYS

We conclude this chapter by discussing how C arrays and compile-time arrays can be used with STL algorithms. This option may be useful for legacy applications. Some examples are:

```
void Array()
{
    std::cout << "Fixed-size arrays\n";
    const std::size_t N = 10;
    std::array<double, N> a = { 1,2,3,4 }; a[N - 1] = 3.14;
    Print(a);

    // Copy
    std::vector<double> v1(a.size());
    std::copy(std::begin(a), std::end(a), std::begin(v1));
    Print(v1);
```

```
std::array<double, N> a2;
for (std::size_t i = 0; i < a2.size(); ++i)
    a2[i] = static_cast<double>(i);
Print(a2);

// Copy
std::copy(std::begin(v1), std::end(v1), std::begin(a2));
Print(a2);

// Move
std::array<double, N> a3 = std::move(a2);
Print(a2);
Print(a3);

// Removing duplicates, C arrays
int src[] = { 1, 1, 1, 3, 5, 5, 6, 6, 6 };
std::list<int> myList1;
std::copy(src, src + (sizeof(src) / sizeof(src[0])),
          back_inserter(myList1));
}
```

The output is:

```
Fixed-size arrays
1,2,3,4,0,0,0,0,0,3.14,
1,2,3,4,0,0,0,0,0,3.14,
0,1,2,3,4,5,6,7,8,9,
1,2,3,4,0,0,0,0,0,3.14,
1,2,3,4,0,0,0,0,0,3.14,
1,2,3,4,0,0,0,0,0,3.14,
```

## 17.6 SUMMARY AND CONCLUSIONS

In this chapter we introduced two categories of algorithms; first, *non-modifying algorithms* access the elements of a range without modifying their values or their real-time order in the range while *modifying algorithms* modify the elements of a range. We provided complete machine-readable code and corresponding output. We strongly recommend that you do the exercises. We give a summary of STL as a concept map in Figure 17.1. It is assumed that these concepts are known to you.

## 17.7 EXERCISES AND PROJECTS

- 1. *(Simple Binder Example)*
  In this exercise we examine a simple function of arity three:

```
double func3d(double x, double y, double z)
{
    return x - y + z;
}
```

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_585_0.png)

# FIGURE 17.1 STL components

The objective is to experiment with std::bind along the lines of the examples in Section 17.2 where we discuss binding functions of arity two.

Answer the following questions:

- a) Create functions of arity zero, one, two and three based on the function func3d and examine the output. Experiment with placeholders. Do you get the results that you expect?

- b) Carry out the same exercise as in part a) by defining a function of arity three as a stored lambda function and assigning a universal function wrapper to a lambda function.

- c) An alternative to std::bind is to model bound variables as captured variables and unbound variables as input arguments to a lambda function.
  
  Carry out the experiment with functions of arity three. Compare binders and lambda functions with regard to readability, maintainability and efficiency. In particular, in application code we may have a choice of implementing functions that model PDEs or SDEs in a certain way and a concern is when these functions are called in loops. Are they more or less efficient than calling virtual or pure virtual functions?

- d) Investigate using std::mem_fn (Section 17.2.3) for the examples in this exercise. Which approach do you prefer?

## 2. (Non-modifying Algorithms in C++11, Small Project)

In this exercise we discuss a number of new STL algorithms that are supported in C++11:

- A1: is_permutation(): determines whether two sequences contain the same elements, albeit in a different order. There are two variants, the second of which takes a comparator function. Complexity is at worst quadratic.

- A2: is_sorted(): determines if elements in a range are sorted. There are four variants.
