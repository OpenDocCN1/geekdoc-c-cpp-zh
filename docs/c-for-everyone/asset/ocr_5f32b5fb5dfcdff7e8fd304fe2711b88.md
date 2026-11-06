```
```
64 int main()
65 {
66    string response;
67    cout << boolalpha; // Show Boolean values as true, false
68
69
70    Question q1;
71    q1.set_text("Who was the inventor of C++?");
72    q1.set_answer("Bjarne Stroustrup");
73
74    q1.display();
75    cout << "Your answer: ";
76    getline(cin, response);
77    cout << q1.check_answer(response) << endl;
78
79    return 0;
80 }
```
```

**Program Run**

```
Who was the inventor of C++?
Your answer: Bjarne Stroustrup
true
```

![](bbox=[0.085, 0.39, 0.248, 0.48])

+   1. Consider classes Manager and Employee. Which should be the base class and which should be the derived class?
+   2. What are the inheritance relationships between classes BankAccount, Checking-Account, and SavingsAccount?
+   3. Consider the function do_something(istream& stream). List all stream classes from Figure 2 whose objects can be passed to this function.
+   4. Consider the function do_something(Car& c). List all vehicle classes from Figure 1 whose objects cannot be passed to this function.
+   5. Should a class Quiz inherit from the class Question? Why or why not?

**Practice It** Now you can try these exercises at the end of the chapter: R10.1, R10.2, R10.5.

# ## 10.2 Implementing Derived Classes

In C++, you form a derived class from a base class by specifying what makes the derived class different. You define the member functions that are new to the derived class. The derived class inherits all member functions from the base class, but you can change the implementation if the inherited behavior is not appropriate.

The derived class automatically inherits all data members from the base class. You only define the added data members.

Here is the syntax for the definition of a derived class:

```
```
class ChoiceQuestion : public Question
{
public:
   New and changed member functions
private:
   Additional data members
};
```
```