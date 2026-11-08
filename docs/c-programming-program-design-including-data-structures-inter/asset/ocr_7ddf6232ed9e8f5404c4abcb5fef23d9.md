25. Consider the following definition of the class `myClass`:

```
~~~cpp
class myClass
{
public:
    void setX(int a);
    //Function to set the value of x.
    //Postcondition: x = a;
    void printX() const;
    //Function to output x.
    static void printCount();
    //Function to output count.
    static void incrementCount();
    //Function to increment count.
    //Postcondition: count++;
    myClass(int a = 0);
    //constructor with default parameters
    //Postcondition x = a;
    //If no value is specified for a, x = 0;

private:
    int x;
    static int count;
};
~~~
```

+   a. Write a C++ statement that initializes the member variable `count` to 0.
+   b. Write a C++ statement that increments the value of `count` by 1.
+   c. Write a C++ statement that outputs the value of `count`.
+   d. Write the definitions of the functions of the class `myClass` as described in its definition.
+   e. Write a C++ statement that declares `myObject1` to be a `myClass` object and initializes its member variable `x` to 5.
+   f. Write a C++ statement that declares `myObject2` to be a `myClass` object and initializes its member variable `x` to 7.
+   g. Which of the following statements are valid? (Assume that `myObject1` and `myObject2` are as declared in Parts e and f.)
+   
+      ~~~cpp
+      myObject1.printCount();       //Line 1
+      myObject1.printX();           //Line 2
+      myClass.printCount();         //Line 3
+      myClass.printX();             //Line 4
+      myClass::count++;             //Line 5
+      ~~~
+   
+   h. Assume that `myObject1` and `myObject2` are as declared in Parts e and f. What is the output of the following C++ code?
+   
+      ~~~cpp
+      myObject1.printX();
+      cout << endl;
+      myObject1.incrementCount();
+      myClass::incrementCount();
+      ~~~