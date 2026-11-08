```
```cpp
isObject >> ch;                         //Step c
isObject >> complex.imaginaryPart;      //Step d
isObject >> ch;                         //Step e

return isObject;    //return the istream object
}
```
```

The definitions of the other functions are as follows:

```
```cpp
bool complexType::operator==
                    (const complexType& otherComplex) const
{
    return (realPart == otherComplex.realPart &&
            imaginaryPart == otherComplex.imaginaryPart);
}

        //Constructor
complexType::complexType(double real, double imag)
{
    realPart = real;
    imaginaryPart = imag;
}

        //Function to set the complex number after the object
        //has been declared.
void complexType::setComplex(const double& real,
                             const double& imag)
{
    realPart = real;
    imaginaryPart = imag;
}

void complexType::getComplex(double& real, double& imag) const
{
    real = realPart;
    imag = imaginaryPart;
}

        //overload the operator +
complexType complexType::operator+
                    (const complexType& otherComplex) const
{
    complexType temp;

    temp.realPart = realPart + otherComplex.realPart;
    temp.imaginaryPart = imaginaryPart
                       + otherComplex.imaginaryPart;

    return temp;
}
```
```