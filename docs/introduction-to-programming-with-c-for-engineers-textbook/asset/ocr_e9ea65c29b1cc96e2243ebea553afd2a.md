```
```cpp
double to_val {};

wcout << L"Enter from currency code:"; wcin >> from_curr; wcout << endl;
wcout << L"Enter value to exchange:"; wcin >> from_val; wcout << endl;
wcout << L"Enter to currency code :"; wcin >> to_curr; wcout << endl;

if( currencyExchangerObj.Convert( from_curr, stod( from_val ),
                                  to_curr, to_val ) == true )
    wcout << from_val << L" " + from_curr + L" => " << to_val
          << L" " + to_curr << endl;
else
    wcout << L"Cannot convert these currencies" << endl;
}
catch( ... )
{
    wcout << L"Error - wrong input." << endl;
}

// Ask the user what to do next
wcout << endl << L"New conversion [y/n]?";
wcin >> answer;
wcout << endl;

} while( answer.find( L"y" ) != wstring::npos );

}
```
```

UserInterface operates in a do-while loop, starting on line [79]. On lines [81–96], inside the loop, a try-catch statement is set to intercept a potential exception object thrown from the called functions. One of them is stod, called on line [91] to convert string to a double value.

On line [112], the Run function is defined, taking the TCurrencyExchanger object. It simply calls three functions we have already seen: DisplayCurrentTime [115], DisplayAllCurrencies [118], and UserInterface [120]:

```
```cpp
// Run if we already have the currency exchanger object
void Run( const TCurrencyExchanger & currExchObj )
{
    wcout << L"*** Welcome to the currency exchanger ***" << endl;
    DisplayCurrentTime();
    wcout << endl;

    DisplayAllCurrencies( currExchObj );

    UserInterface( currExchObj );
}
```
```

The other overloaded function, Run, is defined on line [123]. This time, it internally creates the TCurrencyExchanger object by calling CreateCurExchanger. As we already pointed out, to create it, an initialization file is necessary. This is accessed on line [125] with std::filesystem²⁴ and by creating iniPath on line [127]. (Further details about the C++ filesystem are presented