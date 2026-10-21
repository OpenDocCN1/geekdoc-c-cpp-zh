```
sum += *pstart++;

Console::WriteLine(L"Total of data array elements = {0}\n", sum);

// Just to show we can - access strings through an interior pointer
array<String^>^ strings = { L'Land ahoy!',
                            L"Splice the mainbrace!",
                            L"Shiver me timbers!",
                            L"Never throw into the wind!"
                          };

for(interior_ptr<String^> pstrings = &strings[0] ;
        pstrings-&strings[0] < strings->Length ; ++pstrings)
    Console::WriteLine(*pstrings);

return 0;
}
```

The output from this example is:

```
Total of data array elements = 18

Land ahoy!
Splice the mainbrace!
Shiver me timbers!
Never throw into the wind!
Press any key to continue . . .
```

# How It Works

After creating the data array of elements of type double, you define two interior pointers:

```
interior_ptr<double> pstart = &data[0];
interior_ptr<double> pend = &data[data->Length - 1];
```

The first statement creates pstart as a pointer to type double and initializes it with the address of the first element in the array, data[0]. The interior pointer, pend, is initialized with the address of the last element in the array, data[data->Length - 1]. Because data->Length is the number of elements in the array, subtracting 1 from this value produces the index for the last element.

The while loop accumulates the sum of the elements in the array:

```
while(pstart <= pend)
    sum += *pstart++;
```

The loop continues as long as the interior pointer, pstart, contains an address that is not greater than the address in pend. You could equally well have expressed the loop condition as !pstart > pend.

Within the loop pstart starts out containing the address of the first array element. The value of the first element is obtained by dereferencing the pointer with the expression *pstart and the result of this is added to sum. The address in the pointer is then incremented using the ++ operator. On the last loop iteration, pstart contains the address of the last element which is the same as the address value that pend