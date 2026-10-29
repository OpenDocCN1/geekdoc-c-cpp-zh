# Display 19.14 Program Using the map Template Class (part 2 of 2)

```
Mars - The Red Planet
Mercury - Hot planet
Neptune - 1500 mile-per-hour winds
Pluto - Dwarf planet
Saturn - Has rings
Uranus - Tilts on its side
Venus - Atmosphere of sulfuric acid
```

# TIP: Use Initialization, Ranged for, and auto with Containers

Several features introduced in C++11 make it easier to work with collections. In particular, you can initialize your container objects using the uniform initializer list format, which consists of initial data in curly braces. You can also use auto and the ranged for loop to easily iterate through a container. Consider the following two initialized collection objects:

```
map<int, string> personIDs = {
    {1,"Walt"},
    {2,"Kenrick"}
};
```

```
set<string> colors = {"red","green","blue"};
```

We can iterate conveniently through each container using a ranged for loop and auto:

```
for (auto p : personIDs)
    cout << p.first << " " << p.second << endl;
for (auto p : colors)
    cout << p << " ";
```

The output of these lines is

```
1 Walt
2 Kenrick
blue green red
```

# Self-Test Exercises

+   14. Why are the elements in the set template class stored in sorted order?
+   15. Can a set have elements of a class type?
+   16. Suppose s is of the type set<char>. What value is returned by s.find('A') if 'A' is in s? What value is returned if 'A' is not in s?
+   17. How many elements will be in the map mymap after the following code executes?
+   map<int, string> mymap;
+   mymap[5] = "c++";
+   cout << mymap[4] << endl;