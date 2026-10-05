# Display 19.14 Program Using the map Template Class (part 2 of 2)

```
Iterating through all planets:
Earth - Home
Jupiter - Largest planet in our solar system
Mars - The Red Planet
Mercury - Hot planet
Neptune - 1500 mile-per-hour winds
Pluto - Dwarf planet
Saturn - Has rings
Uranus - Tilts on its side
Venus - Atmosphere of sulfuric acid
```

![](bbox=[0.052, 0.356, 0.173, 0.373])

# Self-Test Exercises

+   14. Why are the elements in the set template class stored in sorted order?
15. Can a set have elements of a class type?
16. Suppose s is of the type set<char>. What is returned by s.find('A') if 'A' is in s? What value is returned if 'A' is not in s?
17. How many elements will be in the map mymap after the following code executes?

```
map<int, string> mymap;
mymap[5] = "C++";
out << mymap[4] << endl;
```

# 19.3 Generic Algorithms

LEWIS CARROLL, Through the Looking-Glass

This section covers basic function templates in the STL. We cannot give you a comprehensive description of all here, but we will present a large enough sample to give you a good feel for what is contained in the STL and you sufficient detail to start using these template functions.

These template functions are sometimes called generic algorithms. The term algorithm is used for a reason. Recall that an algorithm is just a set of instructions for performing a task. An algorithm can be presented in any language, including a programming language like C++. But, when using the word algorithm, programmers typically have in mind a less formal presentation given in English or pseudocode. As such, it is often thought of as an abstraction of the code defining a function.