allows one to overload the + operator so that it can be used with a particular form of structure or class. Chapter 11 discusses this facility.A template that requires using the + operator could handle a structure that had an overloaded + operator.Another approach is to provide specialized template definitions for particular types. Let’s look at that next.

# Explicit Specializations

Suppose you define a structure like the following:

```
{
  char name[40];
  double salary;
  int floor;
};
```

Also suppose you want to be able to swap the contents of two structures.The original template uses the following code to effect a swap:

```
temp = a;
a = b;
temp = a;
```

Because C++ allows you to assign one structure to another, this works fine, even if type T is a job structure.But suppose you only want to swap the salary and floor members, keeping the name members unchanged.This requires different code, but the arguments to Swap () would be the same as for the first case (references to two job structures), so you can’t use template overloading to supply the alternative code.

However, you can supply a specialized function definition, called an explicit specialization, with the required code. If the compiler finds a specialized definition that exactly matches a function call, it uses that without looking for templates.
The mechanism has changed with the evolution of C++.We’ll look at the current form as mandated by the C++ Standard.

# Third-Generation Specialization (ISO/ANSI C++ Standard)

After some youthful experimentation with other approaches, the C++98 Standard settled on this approach:

+   - For a given function name, you can have a non template function, a template function, and an explicit specialization template function, along with overloaded versions of all of these.
- The prototype and definition for an explicit specialization should be preceded by template <> and should mention the specialized type by name.
- A specialization overrides the regular template, and a non template function overrides both.