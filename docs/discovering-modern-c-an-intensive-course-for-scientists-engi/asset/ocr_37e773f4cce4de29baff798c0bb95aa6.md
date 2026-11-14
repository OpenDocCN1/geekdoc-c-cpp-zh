![](bbox=[0.365, 0.095, 0.595, 0.395])

# Figure 6-3: Memory layout of math_student

To illustrate the before-mentioned ambiguity, we call person::all_info within math_student:

```
=> c++11/oop/multi2.cpp
```

```
class math_student : ...
{
    virtual void all_info() const override {
        person::all_info();
    }
};
```

This causes the following (reformatted) complaint:

```
.... error: ambiguous conversion from derived class
    'const math_student' to base class 'person';
class math_student -> class student -> class person
class math_student -> class mathematician -> class person
person::all_info();
```

with clang 3.4. We will of course encounter the same problem with every function or data member of super-classes inherited via multiple paths.

# 6.3.2.2 Virtual Base Classes

```
=> c++11/oop/multi3.cpp
```

Virtual Base Classes allow us to store members in common super-classes only once and thus help overcome related problems. However, it requires a basic understanding of the internal implementation to not introduce new problems. In the following example, we just denote person as a virtual base class: