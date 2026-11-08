```
```cpp
SomeData(void)
{
        SomeData();
}

SomeData(int i)
{
        Type = SomeValueDataType::Int;
        Value.iData = i;
}

SomeData(float f)
{
        Type = SomeValueDataType::Float;
        Value.fData = f;
}

SomeData(double d)
{
        Type = SomeValueDataType::Double;
        Value.dData = d;
}
};

int _pmain(int /*argc*/, _pchar* /*argv*/[])
{
        SomeData data = SomeData(2.3F);
        std::wcout << L"Size of SomeData::Value is " << sizeof(data.Value) <<
                L" bytes." << std::endl;

        switch (data.Type)
        {
        case SomeValueDataType::Int:
                std::wcout << L"Int data is " << data.Value.iData << L"," 
                        << std::endl;
                break;
        case SomeValueDataType::Float:
                std::wcout << L"Float data is " << data.Value.fData << L"F," 
                        << std::endl;
                break;
        case SomeValueDataType::Double:
                std::wcout << L"Double data is " << data.Value.dData << L"," 
                        << std::endl;
                break;
        default:
                std::wcout << L"Data type is unknown." << std::endl;
                break;
        }
        return 0;
}
```
```

As you can see, we define an enum that has members representing each of the types of members of the union. We then define a structure that includes both a variable of the type of that enum and then an anonymous union. This gives us all the information we need to determine which type the union is currently holding within one encapsulated package.