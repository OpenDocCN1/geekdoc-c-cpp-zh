A **constexpr** function behaves just like an ordinary function until you use it where a constant is needed. Then, it is calculated at compile time provided its arguments are constant expressions (e.g., **p2**) and gives an error if they are not (e.g., **p1**). To enable that, a **constexpr** function must be so simple that the compiler (every standard-conforming compiler) can evaluate it. In C++11, that means that a **constexpr** function must have a body consisting of a single **return**-statement (like **scale**()); in C++14, we can also write simple loops. A **constexpr** function may not have side effects; that is, it may not change the value of variables outside its own body, except those it is assigned to or uses to initialize.

Here is an example of a function that violates those rules for simplicity:

```
int glob = 9;

constexpr void bad(int & arg)    // error: no return value
{
    ++arg;                        // error: modifies caller through argument
    glob = 7;                     // error: modifies nonlocal variable
}
```

If a compiler cannot determine that a **constexpr** function is “simple enough” (according to detailed rules in the standard), the function is considered an error.

# ## 8.6 Order of evaluation

The evaluation of a program – also called the execution of a program – proceeds through the statements according to the language rules. When this “thread of execution” reaches the definition of a variable, the variable is constructed; that is, memory is set aside for the object and the object is initialized. When the variable goes out of scope, the variable is destroyed; that is, the object it refers to is in principle removed and the compiler can use its memory for something else. For example:

```
string program_name = "silly";
vector<string> v;                    // v is global

void f()
{
    string s;                            // s is local to f
    while (cin>>s && s!="quit") {
        string stripped;                 // stripped is local to the loop
        string not_letters;
```