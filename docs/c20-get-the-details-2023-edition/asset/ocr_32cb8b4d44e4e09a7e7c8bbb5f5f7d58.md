```
```cpp
18 }
19 return "unknown";
20 }
21
22 int main() {
23
24     std::cout << '\n';
25
26     std::cout << "toString(Color::red): " << toString(Color::red) << '\n';
27
28     using Color::green;
29
30     std::cout << "toString(green): " << toString(green) << '\n';
31
32     using enum Color;
33
34     std::cout << "toString(blue): " << toString(blue) << '\n';
35
36     std::cout << '\n';
37
38 }
```
```

The using enum declaration (lines 14 and 32) introduces the enumerators of the scoped enumerations Color into the local scope. From that point on, the enumerators can be used unscoped (lines 15 - 17 and line 34). Additionally, you can also apply a using declaration for a specific enumeration value (line 28).

![](bbox=[0.34, 0.578, 0.66, 0.695])

# ### 4.9.6 Default Member Initializers for Bit Fields

First of all, what is a bit field? Here is the definition from Wikipedia⁸⁰: “A bit field is a data structure used in computer programming. It consists of a number of adjacent computer memory locations which have been allocated to hold a sequence of bits, stored so that any single bit or group of bits within the

⁸⁰https://en.wikipedia.org/wiki/Bit_field