```
Person^ him = gcnew Person(L"Fred", hisHeight, hisWeight);

Weight herWeight = Weight(105, 3);
Height herHeight = Height(5, 2);
Person^ her = gcnew Person(L"Freda", herHeight, herWeight);

Console::WriteLine(L"She is {0}", her->Name);
Console::WriteLine(L"Her weight is {0:F2} kilograms.",
                    her->getWeight().kilograms);
Console::WriteLine(L"Her height is {0} which is {1:F2} meters.",
                    her->getHeight(),her->getHeight().meters);

Console::WriteLine(L"He is {0}", him->Name);
Console::WriteLine(L"His weight is {0}.", him->getWeight());
Console::WriteLine(L"His height is {0} which is {1:F2} meters.",
                    him->getHeight(),him->getHeight().meters);
    return 0;
}
```

This example produces the following output:

```
She is Freda
Her weight is 47.73 kilograms.
Her height is 5 feet 2 inches which is 1.57 meters.
He is Fred
His weight is 185 pounds 7 ounces.
His height is 6 feet 3 inches which is 1.91 meters.
Press any key to continue . . .
```

# How It Works

The two value classes, Height and Weight, define the height and weight of a person. The Person class has fields of type Height and Weight to store the height and weight of a person and the name of a person is stored in the Name property, which is a trivial property because no explicit get() and set() functions have been defined for it; it therefore has the default get() and set() functions.

The first two statements in main() define Height and Weight objects and these are then used to define him:

```
Weight hisWeight = Weight(185, 7);
Height hisHeight = Height(6, 3);
Person^ him = gcnew Person(L"Fred", hisHeight, hisWeight);
```

Height and Weight are value classes so the variables of these types store the values directly. Person is a reference class so him is a handle. The first argument to the Person class constructor is a string literal so the compiler arranges for a String object to be created from this and the handle to this object is passed as the argument. The second and third arguments are the value class objects that you create in the first two statements. Of course, copies of these are passed as arguments because of the pass-by-value mechanism for function arguments. Within the Person class constructor, the assignment statement sets the value of the Name parameter and the values of the two fields, ht and wt, are set in the initialization list. The only way to set a property is through an implicit call of its set() function; a property cannot be initialized in the initializer list of a constructor.