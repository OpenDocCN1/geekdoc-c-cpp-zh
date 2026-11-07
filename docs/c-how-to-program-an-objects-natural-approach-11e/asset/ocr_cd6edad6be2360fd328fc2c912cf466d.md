```
```cpp
20    std::cout << "\n\nAfter concatenations:\n";
21    std::string s4{s1 + "apult"}; // concatenation
22    s1.append("acomb"); // create "catacomb"
23    s3 += "pet"; // create "carpet" with overloaded +=
24    std::cout << std::format("s1: {}\ns2: {}\ns3: {}\ns4: {}\n", s1, s3, s3, s4);
25
26    // append locations 4 through end of s1 to
27    // create string "comb" (s5 has initially empty)
28    std::string s5{}; // initialized to the empty string
29    s5.append(s1, 4, s1.size() - 4);
30    std::cout << std::format("s5: {}\n", s5);
31 }
```
```

```
```text
s1: cat
s2: cat
s3: cat

After changes:
s2: rat
s3: car

After concatenations:
s1: catacomb
s3: carpet
s4: catapult
s5: comb
```
```

**Fig. 8.1** | Demonstrating string assignment and concatenation. (Part 2 of 2.)

# String Assignment

Lines 8–10 create the string variables s1, s2 and s3. Line 12 uses the assignment operator to copy the contents of s1 into s2. Line 13 uses member function assign to copy s1’s contents into s3. This particular version of assign is equivalent to using the = operator, but assign also has many overloads.¹ For example, one overload copies a specified number of characters, as in

```
```cpp
target.assign(source, start, numberOfChars);
```
```

where source is the string to copy, start is the starting index, and numberOfChars is the number of characters to copy.

# Accessing String Elements By Index

Lines 16–17 use the string member function at to assign 'r' to s2 at index 0 (forming "rat") and to assign 'r' to s3 at index 2 (forming "car"). You can also use the member function at to get the character at a specific index in a string. As with std::array and std::vector, a std::string’s at member function performs range checking and throws an out_of_range exception if the index is not within the string’s bounds. The string subscript operator, [], does not check whether the index is in bounds. This is consistent with its use with std::array and std::vector. You can also iterate through the characters in a string using range-based for, as in

1. For details of each, see https://en.cppreference.com/w/cpp/string/basic_string/assign.