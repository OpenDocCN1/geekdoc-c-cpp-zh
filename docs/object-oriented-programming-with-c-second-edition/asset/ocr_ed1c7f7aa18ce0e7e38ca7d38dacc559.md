# 2.1.7 Data Abstraction

The class construct provides facilities to implement data abstraction. Data abstraction is an important concept and should be understood properly. Let us take the example of the LCD projector from the previous chapter. It has member data (light and fan) as well as member functions (switches that operate the light and fan). This real-world object hides its internal operations from the outside world. It, thus, obviates the need for the user to know the possible pitfalls that may be encountered during operation. During its operation, the LCD projector never reaches an invalid state.

Data abstraction is a virtue by which an object hides its internal operations from the rest of the program. It makes it unnecessary for the client programs to know how the data is internally arranged in the object. Thus, it obviates the need for the client programs to write precautionary code when creating and using objects.

Now, in order to understand this concept, let us take an example in C++. The library programmer, who has designed the Distance class, wants to ensure that the finches never exceed 12. If a value larger than 12 is specified by an application programmer calling the Distance::setInches(), the logic incorporated within the definition of the function should automatically increment the value of iFeet and decrement the value of finches by suitable. A modified definition of the Distance::setInches() is as follows.

```
void Distance::setInches(float y)
{
    finches=y;
    if(finches>=12)
    {
        iFeet+=finches/12;
        finches=((int)finches/12)*12;
    }
}
```

Here, we notice that an application programmer need not send values less than 12 when calling the Distance::setInches(). The default logic within the Distance::setInches() function does the necessary adjustments. This is an example of data abstraction.

The above restriction may not appear mandatory. However, we will see later classes where similar restrictions will be absolutely necessary (and also complicated).

Similarly, the definition of the Distance::add() function should also be modified as follows by the library programmer. Here, it can be assumed that the value of finches of neither the invoking object nor the object appearing ('dd') can be greater than 12.

```
Distance Distance::add(Distance dd)
{
    Distance temp;
    temp.iFeet=iFeet+dd.iFeet;
    temp.setInches(finches+dd.finches);
    return temp;
}
```

Now, if we write the statements shown in Listing 2.10