a value. Also, in accordance with the usual practice when displaying addresses, you have used the {0:X} format specifier in the WriteLine commands to ensure that memory addresses are displayed in hexadecimal format.

Finally, you use the pointer pX to change the value of x to 20 and do some pointer casting to see what happens if you try to treat the content of x as if it were a double.

Compiling and running this code results in the following output:

```
Address of x is 0x376943D5A8, size is 4, value is 10
Address of y is 0x376943D5A0, size is 2, value is -1
Address of y2 is 0x376943D598, size is 1, value is 4
Address of z is 0x376943D590, size is 8, value is 1.5
Address of pX=&x is 0x376943D588, size is 8, value is 0x376943D5A8
Address of pY=&y is 0x376943D580, size is 8, value is 0x376943D5A0
Address of pZ=&z is 0x376943D578, size is 8, value is 0x376943D590
After setting *pX, x = 20
*pX = 20
x treated as a double = 9.88131291682493E-323
```

> NOTE When you run the application with the CoreCLR, different addresses are shown every time you run the application.

Checking through these results confirms the description of how the stack operates presented in the “Memory Management Under the Hood” section earlier in this chapter. It allocates successive variables moving downward in memory. Notice how it also confirms that blocks of memory on the stack are always allocated in multiples of 4 bytes. For example, y is a short (of size 2) and has the (hex) address 0xD4E710, indicating that the memory locations reserved for it are locations 0xD4E710 through 0xD4E713. If the .NET runtime had been strictly packing up variables next to each other, y would have occupied just two locations, 0xD4E712 and 0xD4713.

The next example illustrates pointer arithmetic, as well as pointers to structs and class members. This example is named PointerPlayground2. To start, you define a struct named CurrencyStruct, which represents a currency value as dollars and cents. You also define an equivalent class named CurrencyClass (code file PointerPlayground2/Currency.cs):

```
internal struct CurrencyStruct
{
    public long Dollars;
    public byte Cents;

    public override string ToString() => $"${Dollars}.{Cents}";
}

internal class CurrencyClass
{
    public long Dollars = 0;
```