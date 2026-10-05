
marked as const due to the automatic insertion. This is demonstrated in Listing 24.67.

```
// https://cppbolt.org/z/Ejsjsx4Ta
string search(const map<int,string>&data) {
    return data[7];    // non-const method on const parameter
}
string search5(const map<int,string>&data) {
    auto it=data.find(5); // not automatically inserting
    return it==data.end() ? string() : it->second;
}
// -
map<int,string> dwarfs={1,"one"}, {3,"three"}, {5,"five"}, {7,"seven"};
cout << search7(dwarfs) << "\n";
cout << search5(dwarfs) << "\n"; // Output: five
```

**Listing 24.67** You cannot use "operator[]" on a const map.

# Deleting

Deleting in map is hardly different from deleting in set:

- * Deleting all elements*
clear() clears the map completely.

- * Deleting a single element*
erase deletes a single element by iterator or with a key.

- * Transferring a single element*
extract removes an element that you want to put elsewhere by insert.

- * Deleting multiple of elements*
Using a pair of iterators for erase, you delete multiple elements.

After deletion, iterators in the container are still valid if their elements were not affected by the deletion.

# Specialty: "operator[]"

Among the associative containers, only map offers the index operator[]. This greatly simplifies the use of map, and source code with maps looks compact and readable.

However, it has a peculiarity that you really need to remember. It automatically inserts a new element into the container if there is no entry for the key yet. I have already demonstrated this with several examples, such as in Listing 24.59, Listing 24.64, and Listing 24.67, but I cannot emphasize it enough.

A multiset, like a set (Section 24.7.3, ...), contains elements that are also keys, which you can quickly search for. The difference is that elements can also occur multiple times. So, if you insert the value 7 three times into a multiset<int>, you will get three sevens when iterating through it. `insert` and `emplace` will always add one or more elements. The behavior of the search functions adapts accordingly. The returns of `lower_bound`, `upper_bound`, and `equal` range now point to the edges of the range with matching elements. `find` returns any matching element. `erase`, when called with a (key) element, deletes all matching elements, not just one.

merge removes all elements from the source, instead of leaving duplicates behind.

If you want to use multiset, you need #include<set>.

The examples for multiset should be considered embedded in Listing 24.68.

```
// https://github.com/cpp/z/aMI87neG6
#include <set>    // multiset
#include <iostream>
using std::multiset; using std::cout;
template<typename Elem, typename Comp>
std::ostream& operator<<=(std::ostream&os, const multiset<Elem,Comp>&data) {
    for(const auto& e : data) {
        os << e << ' ';
    }
    return os << '\n'; // '\n' instead of '\'' for line break
}

int main() {
    // Example code here
}
```

**Listing 24.68** This is the template for the example listings in this section on "multiset".

Note my comment on << in the box that followed Listing 24.12.

# The Elements and Their Properties

As with set, the elements in the multiset are the keys by which the container is kept sorted. Here too, you can overload operator<= or operator> for your element type, or provide your own comparator as an optional template argument.

To make it clear, so that there are no misunderstandings, especially not in comparison to the unordered multiset: all elements in the multiset are stored in a sorted tree, including duplicates. You can see this exemplified in Figure 24.12. It is not the case that duplicates are stored in a linked list or something similar. This means that even with a multimap having many or duplicate entries, the performance does not degrade. The key property of multiset is that its efficiency is guaranteed and unlike unordered_multiset if they have poor hash functions. In Listing 24.75, you can see how set, multiset, and unordered_multiset perform in different scenarios. One conclusion is that many identical elements do not degrade the performance. An alternative is flat_multiset from C++23, which stores the elements sorted in a vector. Check this especially with many containers or very small elements.

# Initialize

A multiset has exactly the same construction options as set:

- Without arguments via default constructor
- A range from another container using pair of iterators
- Another container for copying
- From C++23, a constructor with from_range

In many cases, the compiler can deduce the template parameters from the constructor arguments if you are using C++17. If you choose an initializer list from another container, you get a container that contains the elements sorted and retains duplicate entries.

```
// https://godbolt.org/z/agkdB
#include <vector>
multiset ms{1,2,3}; // sorted at initialization
cout << ms{7,7,7,7,7}; // Output: 1 2 3
std::set range(ms.begin(), ms.end()); // set removes duplicates
cout << range.size() << ": " << *range.begin(); // Output: 3
multiset msrange(ms.begin(), ms.end()); // multiset retains duplicates
cout << msrange; // Output: 7 7 7 7
```

**Listing 24.69** Entries are sorted, and duplicates are retained.

# Assignment

With operator=, you can reassign the contents of multiset just like a set, either by copy or move. The swap method is also used here to implement idioms.

# Insert

You insert into multiset using the same overloads as in set, with one exception: where set returns pair<iterator,bool> to indicate whether an insertion took place, multiset only returns the iterator. Finally, multiset always inserts, regardless of whether the element exists or not:

- Inserting a single element with automatic positioning
Use insert to insert a single value by copy, or emplace to create the element directly in place. The return is a single iterator—unlike set, multiset inserts in O(log n) time, regardless of whether the element is already present or not.

- Inserting a single element with a position hint
If you provide an iterator along the value to be inserted, multiset also tries to interpret this iterator as a hint for insertion. If you do not want to pass a value but create it in place, use emplace_hint. You also know from set, and here too the amortized time complexity is O(1) if the hint is correct, and O(log n) if not.

- Inserting multiple elements
Like set, multiset also understands inserting multiple elements at once if you provide an initializer list or multiple via iterator pair. From C++23 onward, there is also insert_range. As expected with multiset, all elements are transferred, including duplicates.

As with set, all iterators of the container remain valid after an insertion in multiset.

# Accessing

The interface of multiset for accessing is identical to of set. Only the duplicate elements in the container need to be accounted for in the returns. Either they return any matching element or encompass the entire range of matching elements:

- Access via iterators
You use the variants of begin() and end() that you know from set to obtain bidirectional iterators.

- Access via search
If find finds the search element in the container, then it is any of the matching elements. This is different with lower_bound, upper_bound, and equal_range, because with the specification already introduced in set, you get the area boundaries of all matching elements of the container. Here, count is interesting because the number of found elements has more informational value in this case.

- Searching without a specific key
You can save the creation of a concrete search key during the search if you use a suitable comparison functor with is_transparent, as shown for set in Listing_24.70.

The following lists some examples of accessing a multiset.

```
// https://cppreference.org/w/multiset
#include <string>
#include <iterator>
#include <ranges>
#include <set>

struct Person {
    std::string name;
    friend bool operator<(const Person &a, const Person &b) {
        // only first letter
        return a.name.size() == b.name.size() ? true : a.name[0] < b.name[0];
    }
};

multiset<int> data = {1, 4, 4, 2, 2, 7, 9};
auto [from1, tol] = data.equal_range(2);
cout << "Number of 2: " << std::distance(from1, tol) << '\n';
auto [from2, to2] = data.equal_range(5);
cout << "Number of 5: " << '\n';
cout << std::distance(from2, to2) << '\n'; // Output: Number of 5s: 0
multiset<Person> person = {
    {"Karl", "Kurt"}, {"Karl", "Ken"};
auto [p, q] = std::ranges::subrange(person, "K");
for(auto& p : std::ranges::subrange(p, q)) { // C++20 range or simple loop
    cout << p.name << '\n';
}
cout << '\n'; // Output: Karl Kurt Karl Ken
```

**Listing 24.70** "multiset" search functions find the range of matching elements.
