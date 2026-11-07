# **Program 11.31**  File app.cpp (Continued)

```
```cpp
12    // Instantiation of tokenizer object
13    Tokenizer tokenizer (target, delimit);
14    // Traversing the target string to find tokens
15    while (tokenizer.moreToken())
16    {
17        cout << tokenizer.nextToken() << endl;
18    }
19    return 0;
20 }
```
```

```
```text
Run:
This
is
the
string
to
be
tokenize.
```
```

# ### 11.4.2 Registration

In this section we use association and dependency between classes to design a simple registration system for a small department in a college or university.

# ### UML Class Diagram

We use six classes as shown in Figure 11.27.

Each *student* object composes a *string* object (as student name) and composes a *schedule* object, which in turn composes an array of student names (strings). Each *course* object composes a *string* object (as course name) and composes a *roster* object, which in turn composes an array of course names (strings). The registrar class just uses the *student* and *course* objects.

# ### UML Sequence Diagram

Before writing the code for the five user-defined classes involved, we show the sequence diagram and the interaction between the classes (Figure 11.28). Note that the *roster* object

![](bbox=[0.315, 0.735, 0.766, 0.904])

Figure 11.27  Relationship among classes in registration project