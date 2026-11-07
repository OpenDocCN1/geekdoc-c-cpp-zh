

- 1. 打开输入文件和输出文件。
- 2. 如果输入文件不存在，则退出程序。
- 3. 读取秘密代码的长度。
- 4. 如果秘密代码的长度大于 250，则终止程序，因为本程序中代码的最大长度为 250。
- 5. 读取秘密代码并将其存储到数组中。
- 6. 读取副本的长度。
- 7. 如果秘密代码及其副本的长度相同，则比较这些代码并输出相应消息。否则，打印错误消息。

为了简化函数 main，我们编写一个函数 readCode 来读取秘密代码，并编写另一个函数 compareCode 来比较这些代码。

### readCode

该函数首先读取秘密代码的长度。如果秘密代码的长度大于 250，则将 bool 变量 lenCodeOk（它是一个引用参数）设为 false，并终止该函数。lenCodeOk 的值会传递给调用函数，以指示是否成功读取了秘密代码。如果代码长度小于 250，则 readCode 函数读取秘密代码并将其存储到数组中。由于输入存储在文件中，且该文件是在函数 main 中打开的，因此与输入文件对应的输入流变量必须作为参数传递给该函数。此外，在读取秘密代码的长度和代码本身之后，readCode 函数必须将这些值传递给函数 main。因此，该函数有四个参数：一个输入文件流变量、一个用于存储秘密代码的数组、代码长度以及 bool 参数 lenCodeOk。函数 readCode 的定义如下：

```cpp
void readCode(ifstream& infile, int list[], int& length,
              bool& lenCodeOk)
{
    lenCodeOk = true;

    infile >> length;   //get the length of the secret code

    if (length > MAX_CODE_SIZE)
    {
        lenCodeOk = false;
        return;
    }

    //Get the secret code.
    for (int count = 0; count < length; count++)
        infile >> list[count];
}
```

### compareCode

该函数将秘密代码与其副本进行比较。因此，它必须能够访问包含秘密代码的数组以及秘密代码的长度。秘密代码的副本及其长度存储在输入文件中。因此，与输入文件对应的输入流变量必须作为参数传递给该函数。此外，compareCode 函数会比较秘密代码与副本，并打印相应消息。由于输出将存储在文件中，与输出文件对应的输出流变量也必须作为参数传递给该函数。因此，该函数有四个参数：一个输入文件流变量、一个输出文件流变量、包含秘密代码的数组以及秘密代码的长度。上述讨论可转化为函数 compareCode 的以下算法：

- a. 声明变量。
- b. 将 `bool` 变量 `codeOk` 设为 `true`。
- c. 读取秘密代码副本的长度。
- d. 如果秘密代码及其副本的长度不相同，则输出相应的错误消息并终止该函数。
- e. 对于输入文件中的每一位数字：
  - 1. 读取秘密代码副本的下一位数字。
  - 2. 输出秘密代码及其副本中的对应数字。
  - 3. 如果对应数字不相同，则输出错误消息，并将 `bool` 变量 `codeOk` 设为 `false`。
- f. 如果 `bool` 变量 `codeOk` 为 `true`：
  输出一条消息，表明秘密代码已正确传输。
  
  否则
  
  输出错误消息。

按照该算法，函数 compareCode 的定义如下：

```cpp
void compareCode(ifstream& infile, ofstream& outfile,
                 const int list[], int length)
{
        //Step a
        int length2;
        int digit;
        bool codeOk;

        codeOk = true;                         //Step b

        infile >> length2;                     //Step c

        if (length != length2)                         //Step d
        {
            cout << "The original code and its copy "
                 << "are not of the same length."
                 << endl;
            return;
        }

        outfile << "Code Digit    Code Digit Copy"
                << endl;

        for (int count = 0; count < length; count++)    //Step e
        {
            infile >> digit;
            outfile << setw(5) << list[count]           //Step e.1
                    << setw(17) << digit;              //Step e.2

            if (digit != list[count])                   //Step e.3
            {
                outfile << "  The code digits are not the same"
                        << endl;
                codeOk = false;
            }
            else
                outfile << endl;
        }

        if (codeOk)                                     //Step f
            outfile << "Message transmitted OK."
                    << endl;
        else
            outfile << "Error in transmission. "
                    << "Retransmit!!" << endl;
}
```

以下是函数 main 的算法：

## 主算法

- 1. 声明变量。
- 2. 打开文件。
- 3. 调用函数 `readCode` 读取秘密代码。
- 4. `if`（秘密代码长度 <= 250）
  调用函数 `compareCode` 比较这些代码。
- 5. `else`
  输出相应的错误消息。

```cpp
{
    cout << "Cannot open the input file." << endl;
    return 1;
}

cout << "Enter the output file name: ";
cin >> outputFile;
cout << endl;

outcode.open(outputFile);

readCode(incode, codeArray, codeLength,
         lengthCodeOk);                    //Step 3

if (lengthCodeOk)                          //Step 4
    compareCode(incode, outcode, codeArray,
                codeLength);
else
    cout << "Length of the secret code "
         << "must be <= " << MAX_CODE_SIZE
         << endl;                          //Step 5

incode.close();
outcode.close();

return 0;
}

//Place the definitions of the functions readCode and
//compareCode, as described previously, here.
```

**示例运行：** 在此示例运行中，用户输入以阴影表示。

请输入输入文件名：`Ch8_SecretCodeData.txt`

请输入输出文件名：`Ch8_SecretCodeOut.txt`

**输入文件数据：**（Ch8_SecretCodeData.txt）

7 9 2 7 8 3 5 6 7 9 2 7 8 3 5 6

**输出文件数据：**（Ch8_SecretCodeOut.txt）

| 代码数字 | 代码数字副本 |
|---:|---:|
| 9 | 9 |
| 2 | 2 |
| 7 | 7 |
| 8 | 8 |
| 3 | 3 |
| 5 | 5 |
| 6 | 6 |

消息传输正常。

该程序的算法如下：

- 1. 声明变量。
- 2. 打开输入文件和输出文件。
- 3. 初始化变量。
- 4. 当输入文件中还有更多数据时：
  - 4.1 对于一行中的每个字符：
    - 4.1.1 读取并写入该字符。
    - 4.1.2 增加相应字母的计数。
  - 4.2 增加行计数。
- 5. 输出行计数和字母计数。
- 6. 关闭文件。

为了简化函数 `main`，我们将其划分为四个函数：

- 函数 `initialize`
- 函数 `copyText`
- 函数 `characterCount`
- 函数 `writeTotal`

以下各节将详细描述这些函数中的每一个。然后，借助这些函数，我们描述函数 `main` 的算法。

### initialize

该函数将变量 `lineCount` 和数组 `letterCount` 初始化为 0。因此，它有两个参数：一个对应于变量 `lineCount`，另一个对应于数组 `letterCount`。显然，对应于 `lineCount` 的参数必须是引用参数。该函数的定义如下：

```cpp
void initialize(int& lc, int list[])
{
    lc = 0;

    for (int j = 0; j < 26; j++)
        list[j] = 0;
} // end initialize
```

### copyText

该函数读取一行并输出该行。读取一个字符后，它调用函数 `characterCount` 来更新字母计数。显然，该函数有四个参数：一个输入文件流变量、一个输出文件流变量、一个 `char` 变量以及用于更新字母计数的数组。

注意，`copyText` 函数并不执行字母计数，但我们仍然将数组 `letterCount` 传递给它。我们采取这一步是因为该函数调用

