The enumerators don’t even need to have unique values. You could define Monday and Mon as both having the value 1, for example, like this:

```
```cpp
enum class Day { Monday = 1, Mon = 1, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday };
```
```

You can now use either Mon or Monday as the first day of the week. A variable, yesterday, that you’ve defined as type Day could then be set with this statement:

```
```cpp
yesterday = Day::Mon;
```
```

You can also define the value of an enumerator in terms of a previous enumerator. Throwing everything you’ve seen so far into a single example, you could define the type Day as follows:

```
```cpp
enum class Day { Monday = 0,                 Mon = Monday,
                 Tuesday = Monday + 2,         Tues = Tuesday,
                 Wednesday = Tuesday + 2,       Wed = Wednesday,
                 Thursday = Wednesday + 2,      Thurs = Thursday,
                 Friday = Thursday + 2,         Fri = Friday,
                 Saturday = Friday + 2,         Sat = Saturday,
                 Sunday = Saturday + 2,         Sun = Sunday
               };
```
```

Now variables of type Day can have values from Monday to Sunday and from Mon to Sun, and the matching pairs of enumerators correspond to the integer values 0, 2, 4, 6, 8, 10, and 12. Values for enumerators must be *compile-time constants*, that is, constant expressions that the compiler can evaluate. Such expressions include literals, enumerators that have been defined previously, and variables that you’ve specified as const. You can’t use non-const variables, even if you’ve initialized them using a literal.

The enumerators can be an integer type that you choose, rather than the default type int. You can also assign explicit values to all the enumerators. For example, you could define this enumeration:

```
```cpp
enum class Punctuation : char { Comma = ',', Exclamation = '!', Question = '?'};
```
```

The type specification for the enumerators goes after the enumeration type name and is separated from it by a colon. You can specify any integral data type for the enumerators. The possible values for variables of type Punctuation are defined as char literals and will correspond to the code values of the symbols. Thus, the values of the enumerators are 44, 33, and 63, respectively, in decimal, which also demonstrates (again) that the values don’t have to be in ascending sequence.

Here’s an example that demonstrates some of the things you can do with enumerations:

```
```cpp
// Ex3_03.cpp
// Operations with enumerations
import <iostream>;
import <format>;

int main()
{
  enum class Day { Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday };
  Day yesterday {Day::Monday }, today{ Day::Tuesday }, tomorrow{ Day::Wednesday };
  const Day poets_day{ Day::Friday };
}
```
```