
# The STL and the string Class

The string class, although not part of the STL, is designed with the STL in mind. For example, it has begin(), end(), rbegin(), and rend() members. Thus, it can use the STL interface. Listing 16.17 uses the STL to show all the permutations you can form from the letters in a word. A permutation is a rearrangement of the elements in a container. The next_permutation() algorithm transforms the contents of a range to the next permutation; in the case of a string, the permutations are arranged in ascending alphabetical order. The algorithm returns true if it succeeds and false if the range is already in the final sequence. To get all permutations of a range, you should start with the elements in the earliest possible order, and the program uses the STL sort().

Listing 16.17 strstl.cpp

```cpp
// strstl.cpp -- applying the STL to a string
#include <iostream>
#include <string>
#include <algorithm>

int main() {
    using namespace std;
    string letters;
    cout << "Enter the letter grouping (quit to quit): ";
    while (cin >> letters && letters != "quit") {
        cout << "Permutations of " << letters << endl;
        sort(letters.begin(), letters.end());
        do {
            cout << letters << endl;
        } while (next_permutation(letters.begin(), letters.end()));
        cout << "Enter next sequence (quit to quit): ";
    }
    cout << "Done.\n";
    return 0;
}
```

Here's a sample run of the program in Listing 16.17:

Enter the letter grouping (quit to quit): awl
Permutations of awl
aw
awl
law
lwa
wal
wla
Enter next sequence (quit to quit): all
Permutations of all
all
lal
lla
Enter next sequence (quit to quit): quit
Done.

Note that the next_permutation() algorithm automatically provides only unique permutations, which is why the output shows more permutations for the word aul and for the word all, which duplicates letters.

# Function Objects (a.k.a. Functors)

## Functions Versus Container Methods

Sometimes you have a choice between an STL method and an STL function. Usually, the method is the best choice. First, it should be better optimized for a particular container. Second, being a member function, it can use a template class's memory management facts and resize a container when needed.

Suppose, for example that you have a list of numbers and you want to remove all instances of a certain value, say 4, from the list. If la is a list<int> object, you can use the la.remove(4);
// remove all 4s from the list

After this method call, all elements with the value 4 are removed from the list, and the list is automatically resized. There is also an STL algorithm called remove()(see Appendix G). Instead of being invoked by an object, it takes range arguments. If lb is a list<int> object, a call to the function could look like this:
remove(lb.begin(), lb.end(), 4);

However, because remove() is not a member, it can't adjust the size of the list. Instead, it makes sure all the non-removed items are at the beginning of the list, and it returns an iterator to the past-the-end value. You can use this iterator to fix the list size. For example, you can use the erase() method to remove a range that describes the part of the list that is no longer needed. Listing 16.18 shows how this works.

Listing 16.18 listrmv.cpp

```cpp
// listrmv.cpp -- applying the STL to a string
#include <iostream>
#include <list>
#include <algorithm>
```

# Chapter 16 The string Class and the Standard Template Library

```cpp
void Show(int);
const int LIM = 10;
int main()
{
  using namespace std;
  int ar[LIM] = {4, 5, 4, 2, 3, 4, 8, 1, 4};
  list<int> la(ar, ar + LIM);
  list<int> lb(la);
  cout << "Original list contents:\n\t";
  for_each(la.begin(), la.end(), Show);
  cout << endl;
  la.remove(4);
  cout << "After using the remove() method:\n\t";
  cout << "la:\n";
  for_each(la.begin(), la.end(), Show);
  cout << endl;
  list<int>::iterator last;
  last = remove(lb.begin(), lb.end(), 4);
  cout << "After using the remove() function:\n\t";
  cout << "lb:\n\t";
  for_each(lb.begin(), lb.end(), Show);
  cout << endl;
  lb.erase(last, lb.end());
  cout << "After using the erase() method:\n\t";
  cout << "lb:\n\t";
  for_each(lb.begin(), lb.end(), Show);
  cout << endl;
  return 0;
}
```

```cpp
void Show(int v)
{
  std::cout << v << " ''";
}
```

Here's the output of the program in Listing 16.18.

Original list contents:
4 5 4 2 3 4 8 1 4

After using the remove() method:
la: 5 2 2 3 8 1

After using the remove() function:
lb: 5 2 2 3 8 1 4 1 4

After using the erase() method:
lb: 5 2 2 3 8 1

As you see, the remove() method reduces the list la from 10 elements to 6 elements. However, list lb still contains 10 elements after the remove() function is applied to it. The last 4 elements are disposable because each is either the value 4 or a duplicate of a value moved farther to the front of the list.

Although the methods are usually better suited, the non-method functions are more general. As you've seen, you can use them on arrays and string objects as well as STL containers, and you can use them with mixed container types—for example, to save data from a vector to a list or set.

# Using the STL

The STL provides a powerful set of algorithms that can be used with any container. These algorithms are categorized into several groups, such as searching, sorting, modifying, nonmodifying, binary operations, and set manipulations. Most of these algorithms are available as templates, meaning they can work with different types of data.

One of the most powerful features of the STL algorithms is their flexibility. Because they operate on iterators, they can be used with any container that provides compatible iterators. This means you can use the same sort algorithm on a vector, a list, or even an array.

For example, the sort() algorithm can be used to sort the elements of a vector:

```cpp
vector<int> v = {5, 2, 9, 1, 5};
sort(v.begin(), v.end());
```

The find() algorithm can be used to search for an element in a range:

```cpp
vector<int> v = {5, 2, 9, 1, 5};
auto it = find(v.begin(), v.end(), 9);
if (it != v.end()) {
    cout << "Element found!" << endl;
}
```

The count() algorithm can be used to count the number of occurrences of a value in a range:

```cpp
vector<int> v = {5, 2, 9, 1, 5};
int n = count(v.begin(), v.end(), 5);
cout << "Element 5 appears " << n << " times." << endl;
```

The reverse() algorithm can be used to reverse the elements in a range:

```cpp
vector<int> v = {5, 2, 9, 1, 5};
reverse(v.begin(), v.end());
```

The STL algorithms are a versatile and powerful tool that can help you write more efficient and readable code. By mastering these algorithms, you can take full advantage of the STL containers.
