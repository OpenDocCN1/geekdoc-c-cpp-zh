```
{
CurrencyConvert objConverter = GetConverter( );

Console.WriteLine(
objConverter.ConvertCurrency ( "USD",
"INR", 50 ));

Console.Read ( );

// Dynamic

dynamic dyobjConverter = GetConverter ( );

Console.WriteLine ( dyobjConverter.
ConvertCurrency ( "USD", "INR", 50 ) );

Console.ReadLine ( );
}

public static CurrencyConvert GetConverter ( )
{

CurrencyConvert objConverter = new
CurrencyConvert ( );

return objConverter;
}
}
```

# Dynamic and Overloading of Methods

In overloaded methods, the runtime determines which functions must be called based on the data type of the input