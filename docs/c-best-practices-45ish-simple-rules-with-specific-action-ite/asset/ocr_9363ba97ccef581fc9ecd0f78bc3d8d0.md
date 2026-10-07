const Everything That's Not constexpr

Using a lambda to initialize a const object.

```
const auto data = [](){}; // no parameters
std::vector<int> result;
// fill result with things.
return result;
}(); // immediately invoked
```

![](bbox=[0.123, 0.306, 0.173, 0.355])

Because of RVO, using a lambda will likely not add any overhead and may increase performance.

Did you make any static variables const in the process?
Then go to the constexpr exercise.

![](bbox=[0.123, 0.463, 0.169, 0.503])

> You probably don't want to make class members const; it can break essential things, and sometimes silently.

# Resources

+   - CppCon 2014: James McNellis & Kate Gregory "Modernizing Legacy C++ Code"1
- CppCon 2019: Jason Turner "C++ Code Smells"2
- The implication of const or reference member variables in C++3
- C++Now 2018: Ben Deane "Easy to Use, Hard to Misuse: Declarative Style in C++"4 (Builds on techniques that make applying const easier.)

^1https://youtube.be/LdxAgMe6DI8
2https://youtube.be/f_tLIQ0wLUM
3https://lesleylai.info/en/const-and-reference-member-variables/
4https://youtube.be/2ouxET5R4