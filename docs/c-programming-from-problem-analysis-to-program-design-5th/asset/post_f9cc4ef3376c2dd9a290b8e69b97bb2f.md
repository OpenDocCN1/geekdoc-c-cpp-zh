
- 5. Consider the following class definition:

    ```cpp
    class circle
    {
    public:
        void print() const;
        void setRadius(double);
        double getRadius();
        double area();
        circle();
        circle(double);

    private:
        double radius;
    };
    ```

    ```cpp
    class cylinder: public circle
    {
    public:
        void print() const;
        void setHeight(double);
        double getHeight();
        double volume();
        double area();
        cylinder();
        cylinder(double, double);

    private:
        double height;
    };
    ```

    Suppose that you have the declaration:

    ```cpp
    cylinder newCylinder;
    ```

    Determine the private members of the object newCylinder.

- 6. Suppose that class three is derived from class two, class two is derived from class one, and each class has instance variables. Suppose that an object of class three enters its scope, so the constructors of these classes will execute. Determine the order in which the constructors of these classes will execute.

- 7. Consider the following class definition:

    ```cpp
    class aClass
    {
    public:
        void print() const;
        void set(int, int);
        aClass();
        aClass(int, int);

    private:
        int u;
        int v;
    };
    ```

    What is wrong with the following class definitions?

    - a.

        ```cpp
        class bClass : public aClass
        {
        public:
            void print();
            void set(int, int, int);

        private:
            int z;
        };
        ```

- b. Write the definition of the default constructor of `xClass` so that the `private` member variables of `xClass` are initialized to 0.

- c. Write the definition of the member function `two` of `yClass` so that the `private` member variable `a` is initialized to the value of the first parameter of `two`, and the `private` member variable `b` is initialized to the value of the second parameter of `two`.

- 10. Explain the difference between the `private` and `protected` members of a class.

- 11. Explain the difference between the `protected` and `public` members of a class.

- 12. Consider the following class definition:

    ```cpp
    class first
    {
    public:
        void setX();
        void print() const;
    protected:
        int y;
        void setY(int a);
    private:
        int x;
    };
    ```

    Suppose that `class second` is derived from `class first` using the statement:

    ```cpp
    class second: private first;
    ```

    Determine which member of `class first` are `private`, `protected`, and `public` in `class second`.

- 13. Assume the declaration of Exercise 12. Suppose that `class third` is derived from `class first` using the statement:

    ```cpp
    class third: protected first;
    ```

    Determine which members of `class first` are `private`, `protected`, and `public` in `class third`.

- 14. Assume the declaration of Exercise 12. Suppose that `class fourth` is derived from `class first` using the statement:

    ```cpp
    class fourth: public first;
    ```

    Determine which members of `class first` are `private`, `protected`, and `public` in `class fourth`.

- 15. Assume the declaration of Exercise 12. Suppose that `class fifth` is derived from `class first` using the statement:

    ```cpp
    class fifth: first;
    ```

    Determine which members of `class first` are private, protected, and public in `class fifth`.

- 16. What is wrong with the following code?

    ```cpp
    class classA
    {
    protected:
        void setX(int a);                 //Line 1
            //Postcondition: x = a;       //Line 2

    private:                              //Line 3
        int x;                             //Line 4
    };
    ...
    int main()
    {
        classA aObject;                   //Line 5

        aObject.setX(4);                  //Line 6
        return 0;                         //Line 7
    }
    ```

- 17. Consider the following code:

    ```cpp
    class one
    {
    public:
        void print() const;
            //Output the values of x and y
    protected:
        void setData(int u, int v);
            //Postcondition: x = u; y = v;
    private:
        int x;
        int y;
    };

    class two: public one
    {
    public:
        void setData(int a, int b, int c);
            //Postcondition: x = a; y = b; z = c;
        void print() const;
            //Output the values of x, y, and z
    private:
        int z;
    };
    ```

    - a. Write the definition of the function `setData` of the `class two`.

    - b. Write the definition of the function `print` of the `class two`.

```cpp
baseClass::baseClass(string s, int a)
{
    str = s;
    x = a;
}
```

```cpp
void derivedClass::print() const
{
    cout << "Derived class: " << y << endl;
    baseClass::print();
}
```

```cpp
derivedClass::derivedClass(string s, int a, int b)
    :baseClass("Hello Base", a + b)
{
    y = b;
}
```

- 19. Consider the following class definitions:

    ```cpp
    class baseClass
    {
    public:
        void print() const;
        int getX() const;
        baseClass(int a = 0);

    protected:
        int x;
    };
    ```

    ```cpp
    class derivedClass: public baseClass
    {
    public:
        void print() const;
        int getResult() const;
        derivedClass(int a = 0, int b = 0);

    private:
        int y;
    };
    ```

    Suppose the definitions of the member functions of these classes are as follows:

    ```cpp
    void baseClass::print() const
    {
        cout << "In base: x = " << x << endl;
    }
    ```

    ```cpp
    baseClass::baseClass(int a)
    {
        x = a;
    }
    ```

check whether the date is valid before storing the date in the member variables. Rewrite the definitions of the function setDate and the constructor so that the values for the month, day, and year are checked before storing the date into the member variables. Add a member function, isLeapYear, to check whether a year is a leap year. Moreover, write a test program to test your class.

- 3. A point in the x-y plane is represented by its x-coordinate and y-coordinate. Design a class, pointType, that can store and process a point in the x-y plane. You should then perform operations on the point, such as setting the coordinates of the point, printing the coordinates of the point, returning the x-coordinate, and returning the y-coordinate. Also, write a program to test various operations on the point.

- 4. Every circle has a center and a radius. Given the radius, we can determine the circle's area and circumference. Given the center, we can determine its position in the x-y plane. The center of the circle is a point in the x-y plane. Design a class, circleType, that can store the radius and center of the circle. Because the center is a point in the x-y plane and you designed the class to capture the properties of a point in Programming Exercise 3, you must derive the class circleType from the class pointType. You should be able to perform the usual operations on the circle, such as setting the radius, printing the radius, calculating and printing the area and circumference, and carrying out the usual operations on the center. Also, write a program to test various operations on a circle.

- 5. Every cylinder has a base and height, wherein the base is a circle. Design a class, cylinderType, that can capture the properties of a cylinder and perform the usual operations on the cylinder. Derive this class from the class circleType designed in Programming Exercise 4. Some of the operations that can be performed on a cylinder are as follows: calculate and print the volume, calculate and print the surface area, set the height, set the radius of the base, and set the center of the base. Also, write a program to test various operations on a cylinder.

- 6. Using classes, design an online address book to keep track of the names, addresses, phone numbers, and dates of birth of family members, close friends, and certain business associates. Your program should be able to handle a maximum of 500 entries.
    - a. Define a class, addressType, that can store a street address, city, state, and ZIP code. Use the appropriate functions to print and store the address. Also, use constructors to automatically initialize the member variables.
    - b. Define a class extPersonType using the class personType (as defined in Example 12-9, Chapter 12), the class dateType (as designed in this chapter's Programming Exercise 2), and the class addressType. Add a member variable to this class to classify the person as a family
