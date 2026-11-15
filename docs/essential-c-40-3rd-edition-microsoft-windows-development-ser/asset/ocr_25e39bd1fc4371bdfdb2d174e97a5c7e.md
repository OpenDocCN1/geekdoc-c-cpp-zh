# TABLE 19.2: InterLock's Synchronization-Related Methods

| Method Signature | Description |
|---|---|
| `public static T CompareExchange<T>( T location, T value, T comparand );` | Checks location for the value in comparand. If the values are equal, it sets location to value and returns the original data stored in location. |
| `public static T Exchange<T>( T location, T value );` | Assigns location with value and returns the previous value. |
| `public static int Decrement( ref int location );` | Decrements location by one. It is equivalent to the -- operator, except Decrement() is thread-safe. |
| `public static int Increment( ref int location );` | Increments location by one. It is equivalent to the ++ operator, except Increment() is thread-safe. |
| `public static int Add( ref int location, int value );` | Adds value to location and assigns location the result. It is equivalent to the += operator. |
| `public static long Read( ref long location );` | Returns a 64-bit value in a single atomic operation. |

Most of these methods are overloaded with additional data type signatures, such as support for long. Table 19.2 provides the general signatures and descriptions. For example, the System.Threading namespace does not include generic method signatures until C# 2.0, although earlier versions do include nongeneric equivalents.

Note that you can use Increment() and Decrement() in place of the synchronized ++ and -- operators from Listing 19.5, and doing so will yield better performance. Also note that if a different thread accessed