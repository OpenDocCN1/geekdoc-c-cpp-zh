```
```cpp
private:
    double realPart;          //variable to store the real part
    double imaginaryPart;     //variable to store the imaginary part
};

            // Definitions of operator- and operator!
complexType complexType::operator-() const
{
    complexType temp = *this;

    temp.imaginaryPart = -temp.imaginaryPart;

    return temp;
}

double complexType::operator!() const
{
    return (pow((realPart * realPart +
                 imaginaryPart * imaginaryPart), 0.5));
}
```
```

+   31. When the class has pointer data members.

+   33. Error in Line 4. A template instantiation can be for only a built-in type or a user-defined type. The word “type” between the angular brackets must be replaced either with a built-in type or a user-defined type.

+   35. a. 12    b. Sunny Day

+   37.
+   
+   ```cpp
+   template <class Type>
+   void swap(Type &x, Type &y)
+   {
+       Type temp;
+       temp = x;
+       x = y;
+       y = temp;
+   }
+   ```

+   39. These statements generate and output a random integer between 10 and 25.

# Chapter 14

+   1. a. false;    b. true;    c. true;    d. false;    e. true;    f. false;    g. false;
+      h. true;    i. false;    j. true;    k. false;    l. true;    m. false

+   3. The program will terminate with an error message.

+   5. At most one.