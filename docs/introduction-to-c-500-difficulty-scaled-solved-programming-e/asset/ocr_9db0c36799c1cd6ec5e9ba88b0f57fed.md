# 254 Introduction to C++

```
flag = 1;
for(i = 0; i < 12; i++)
{
    if(upc[i] < '0' || upc[i] > '9')
    {
        cout << "Error: only digits allowed\n";
        flag = 0;
        break;
    }
    if (flag == 1)
        break;
}
sum = 0;
for(i = 0; i < 11; i+=2)
    sum += upc[i]-'0'; /* Subtract '0' to get the numeric value of the digit character. */
sum *= 3;
for(i = 1; i < 11; i+=2)
    sum += upc[i]-'0';
```

```
chk_dig = 10 - (sum%10);
if(chk_dig == 10)
    chk_dig = 0;
```

```
if(chk_dig == (upc[11]-'0'))
    cout << "Valid barcode\n";
else
    cout << "Wrong check digit. The correct is " << chk_dig << '\n\';
return 0;
```

C.10.22 The data compression algorithm Run Length Encoding (RLE) is based on the assumption that a symbol within the data stream may be repeated many times in a row. This repetitive sequence can be replaced by an integer that declares the number of repetitions and the symbol itself. Write a program that reads a string of less than 100 characters and uses the RLE algorithm to compress it. If digits and characters appear once. For example, the string: fffffmmmm1234jjjjjjjjjj should be compressed to: 3f4m1234jx

```
#include <iostream>
#include <cstring>
using std::cout;
using std::cin;

int main()
{
    char str[100];
    int i, len, cnt;

    cout << "Original text: ";
    cin.getline(str, sizeof(str));
    len = strlen(str);

    cout << "Compressed text: ";
    i = 0;
```