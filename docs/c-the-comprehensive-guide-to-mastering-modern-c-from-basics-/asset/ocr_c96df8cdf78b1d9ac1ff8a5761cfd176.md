little of the internals as possible. So avoid methods like int Year::value().

Nevertheless, there are of course operations that you want to perform. Without operations, a type makes no sense. So far, you have "cheated" by relying on the operations that int provides: input, output, calculation, and so on.

If you now do not want to reveal the internals of your class, you must provide the necessary operations for your data type. This can be a lot of work, but it allows for a strict separation of interface and implementation.

Take Year, for example, you have used the int value() method to use the actually encapsulated int value when you wanted to perform calculations with Year. So you have used the operations actually intended for int for Year. In the Easter example, Year was only about the output, implemented through operator<<.

For other purposes, it might be useful to change the year. This operation is named advance with the following method signature:

```
Year&::advance(const Year &difference);
```

Note that the current value_ of the instance is to be changed here. This then allows the following, example:

```
Year{2024};
year.advance(Year{1});
```