# Chapter 6

```
}
}
    return newData;
}
```

```
// Generic function to list an array
generic<typename T> where T:IComparable
void ListElements(array<T>^ data)
{
    for each(T item in data)
        Console::Write(L"{0,10}", item);
    Console::WriteLine();
}
```

```
int main(array<System::String ^> ^args)
{
    array<double>^ data = {1.5, 3.5, 6.7, 4.2, 2.1};
    Console::WriteLine(L"Array contains:");
    ListElements(data);
    Console::WriteLine(L"\nMaximum element = {0}\n", MaxElement(data));
    array<double>^ result = RemoveElement(MaxElement(data), data);
    Console::WriteLine(L" After removing maximum, array contains:");
    ListElements(result);

    array<int>^ numbers = {3, 12, 7, 0, 10,11};
    Console::WriteLine(L"\nArray contains:");
    ListElements(numbers);
    Console::WriteLine(L"\nMaximum element = {0}\n", MaxElement(numbers));
    Console::WriteLine(L"\nAfter removing maximum, array contains:");
    ListElements(RemoveElement(MaxElement(numbers), numbers));

    array<String>^ strings = {L"Many", L"hands", L"make", L"light", L"work"};
    Console::WriteLine(L"\nArray contains:");
    ListElements(strings);
    Console::WriteLine(L"\nMaximum element = {0}\n", MaxElement(strings));
    Console::WriteLine(L"\nAfter removing maximum, array contains:");
    ListElements(RemoveElement(MaxElement(strings), strings));

    return 0;
}
```

The output from this example is:

Array contains:
    1.5      3.5      6.7      4.2      2.1

Maximum element = 6.7

After removing maximum, array contains:
    1.5      3.5      4.2      2.1

Array contains: