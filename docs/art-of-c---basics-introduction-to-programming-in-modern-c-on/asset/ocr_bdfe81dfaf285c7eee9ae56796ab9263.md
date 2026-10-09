enable it shortly, but for now let's see what enabling the nullable context means.

In any code that is within the enabled nullable context, the traditional (nullable) reference variables become non-nullable. Setting `null` values to these variables will cause the compile time errors. (That is, you cannot even build the program. The compiler won't let you. Note that you cannot have runtime errors from your program unless you can build and run the program first. \U0001f642)

In addition, one can use a new kind of reference types within the enabled nullable context. They are called the "nullable reference types". The naming is obviously confusing since all reference types are nullable in the default/traditional C# as well as in all other similar languages that support the pointer/reference types.

But, note that, within the enabled nullable context in C#, the (normal) reference types are non-nullable. Hence, it seems appropriate to use this name for this "new" kind of reference types. The names make sense only in a particular context.

All nullable reference variables (or, the variables of nullable reference types) should be checked for nullability before using them. Otherwise, the compiler will throw the compile errors or warnings (unless the compiler knows for sure that they cannot be null, e.g., through static analysis).

In theory, by doing this, we can eliminate all potential (run-time) null reference exceptions. Variables of non-nullable reference types cannot be null, and hence there is no possibilities of NPEs. For nullable reference variables, you are forced to check the nullability and do the right thing based on their null check. Otherwise, the compiler will stop you. Hence, again, you cannot have NPEs.

In practice, however, even this solution is not perfect. First of all, the compiler support is not perfect. There are a number of different scenarios where the compiler cannot help you much. Refer to the C# official doc if you are interested. But, more importantly, it is not always easy to tell if a certain variable is guaranteed to be non null. Programs have many interconnected components, one component calls/uses another, etc., and they evolve over time, often maintained by different developers or even different teams.