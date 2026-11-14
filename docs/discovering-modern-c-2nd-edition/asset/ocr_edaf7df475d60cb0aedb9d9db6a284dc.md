```
```cpp
};
private:
    string proved;
};

class math_student
    : public student, public mathematician
{
    public:
        math_student(const string& name, const string& passed,
                     const string& proved)
            : student(name, passed), mathematician(name, proved) {}
        virtual void all_info() const override {
            student::all_info();
            mathematician::all_info();
        }
};
```
```

```
```cpp
int main ()
{
    math_student bob["Robert Robson", "Algebra", "Fermat's Last Theorem"];
    bob.all_info();
}
```
```

The program works properly except for the redundant name information:

Click here to view code image

```
```
[student] My name is Robert Robson
I passed the following grades: Algebra
[person] My name is Robert Robson
I proved: Fermat's Last Theorem
```
```

You as the reader now have two choices: accept this sub-optimal method and keep reading or jump to Exercise 6.7.1 and try to solve it on your own. As a consequence of deriving person twice, this code is

+   - **Redundant**: The `name` is stored twice as illustrated in Figure 6–3.
+   - **Error-prone**: The two values of `name` can be inconsistent.
+   - **Ambiguous**: when accessing `person::name` in `math_student` (if it wasn't `private`).

=> c++11/oop_multi2.cpp