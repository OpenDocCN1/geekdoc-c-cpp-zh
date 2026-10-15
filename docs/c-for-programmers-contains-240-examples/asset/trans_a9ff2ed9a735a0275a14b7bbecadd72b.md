

我们已经讨论过星号（`*`）和加号（`+`）量词的工作方式。问号（`?`）量词匹配其所量化的模式出现零次或一次。包含一个数字的大括号，`{n}`，匹配其所量化模式恰好出现 *n* 次。我们在下一个示例中演示此量词。在大括号中包含的数字后加上逗号，匹配量化模式至少出现 *n* 次。包含两个数字的大括号，`{n,m}`，匹配其所量化模式出现 *n* 到 *m* 次（包含）。所有量词都是贪婪的——它们会尽可能多地匹配模式的出现次数，直到模式无法再匹配为止。如果量词后面跟着一个问号（`?`），则量词变为懒惰，并尽可能少地匹配出现次数，只要能成功匹配即可。

| 量词 | 匹配 |
| --- | --- |
| `*` | 匹配前一个模式出现零次或多次。 |
| `+` | 匹配前一个模式出现一次或多次。 |
| `?` | 匹配前一个模式出现零次或一次。 |
| `{n}` | 匹配前一个模式恰好出现 *n* 次。 |
| `{n,}` | 匹配前一个模式至少出现 *n* 次。 |
| `{n,m}` | 匹配前一个模式出现 *n* 到 *m* 次（包含）。 |

**图 21.3** | 正则表达式中使用的量词。

## 21.7.2 使用正则表达式验证用户输入

图 21.4 中的程序提供了一个更复杂的示例，使用正则表达式验证用户输入的姓名、地址和电话号码信息。

**图 21.4** | 使用正则表达式验证用户输入。

```cpp
1  // Fig. 21.4: Validate.cpp
2  // Validating user input with regular expressions.
3  #include <iostream>
4  using std::cin;
5  using std::cout;
6  using std::endl;
7
8  #include <string>
9  using std::string;
10
11 #include "boost/regex.hpp"
12
13 bool validate( const string &, const string & ); // validate prototype
14 string inputData( const string &, const string & ); // inputData prototype
15
16 int main()
17 {
18     // enter the last name
19     string lastName = inputData( "last name", "[A-Z][a-zA-Z]*" );
20
21     // enter the first name
22     string firstName = inputData( "first name", "[A-Z][a-zA-Z]*" );
23
24     // enter the address
25     string address = inputData( "address",
26        "[0-9]+\\s+([a-zA-Z]+|[a-zA-Z]+\\s[a-zA-Z]+)" );
27
28     // enter the city
29     string city =
30        inputData( "city", "([a-zA-Z]+|[a-zA-Z]+\\s[a-zA-Z]+)" );
31
32     // enter the state
33     string state = inputData( "state",
34        "([a-zA-Z]+|[a-zA-Z]+\\s[a-zA-Z]+)" );
35
36     // enter the zip code
37     string zipCode = inputData( "zip code", "\\d{5}" );
38
39     // enter the phone number
40     string phoneNumber = inputData( "phone number",
41        "[1-9]\\d{2}-[1-9]\\d{2}-\\d{4}" );
42
43     // display the validated data
44     cout << "\nValidated Data\n"
45        << "Last name: " << lastName << endl
46        << "First name: " << firstName << endl
47        << "Address: " << address << endl
48        << "City: " << city << endl
49        << "State: " << state << endl
50        << "Zip code: " << zipCode << endl
51        << "Phone number: " << phoneNumber << endl;
52
53     return 0;
54 } // end of function main
55
56 // validate the data format using a regular expression
57 bool validate( const string &data, const string &expression )
58 {
59     // create a regex to validate the data
60     boost::regex validationExpression = boost::regex( expression );
61     return boost::regex_match( data, validationExpression );
62 } // end of function validate
63
64 // collect input from the user
65 string inputData( const string &fieldName, const string &expression )
66 {
67     string data; // store the data collected
68
69     // request the data from the user
70     cout << "Enter " << fieldName << ": ";
71     getline( cin, data );
72
73     // validate the data
74     while ( !( validate( data, expression ) ) )
75     {
76         cout << "Invalid " << fieldName << ".\n";
77         cout << "Enter " << fieldName << ": ";
78         getline( cin, data );
79     } // end while
80
81     return data;
82 } // end of function inputData
```

```text
Enter last name: Doe
Enter first name: John
Enter address: 123 Some Street
Enter city: Some City
Enter state: Some State
Enter zip code: 12345
Enter phone number: 123-456-7890

Validated Data

Last name: Doe
First name: John
Address: 123 Some Street
City: Some City
State: Some State
Zip code: 12345
Phone number: 123-456-7890
```

程序首先要求用户输入姓氏（第 19 行），通过调用 `inputData` 函数。`inputData` 函数（第 65–82 行）接受两个参数，即正在输入的数据的名称和它必须匹配的正则表达式。该函数提示用户（第 70 行）输入指定数据。然后 `inputData` 通过调用 `validate` 函数（第 57–62 行）检查输入是否格式正确。`validate` 函数（第 57–62 行）接受两个参数——要验证的字符串和它必须匹配的正则表达式。该函数首先使用表达式创建一个 `regex` 对象（第 60 行）。然后它调用 `regex_match` 来确定字符串是否与表达式匹配。如果输入无效，`inputData` 会提示用户再次输入信息。一旦用户输入有效输入，数据将作为字符串返回。程序重复该过程，直到所有数据字段都通过验证（第 19–41 行）。然后我们显示所有信息（第 44–51 行）。

在之前的示例中，我们在一个字符串中搜索与正则表达式匹配的子字符串。在此示例中，我们希望确保每个输入的整个字符串都符合特定正则表达式。例如，我们希望接受 "Smith" 作为姓氏，但不接受 "9@Smith#"。我们在此使用 `regex_match` 而不是 `regex_search`——`regex_match` 只有在整个字符串匹配正则表达式时才返回 true。或者，你也可以使用以 `"^"` 字符开头并以 `"$"` 字符结尾的正则表达式。字符 `"^"` 和 `"$"` 分别表示字符串的开始和结束。两者一起强制正则表达式只有在正在处理的整个字符串匹配时才返回匹配。

第 19 行的正则表达式使用方括号和范围表示法来匹配一个大写首字母，后跟任意大小写字母——a–z 匹配任何小写字母，A–Z 匹配任何大写字母。`*` 量词表示第二个字符范围可能在字符串中出现零次或多次。因此，此表达式匹配由一个大写字母组成，后跟零个或多个附加字母的任何字符串。

记号 `\s` 匹配单个空白字符（第 26、30 和 34 行）。用于 `zipCode` 字符串的表达式 `\d{5}`（第 37 行）匹配任意五个数字。字符 `"|"`（第 26、30 和 34 行）匹配其左侧或右侧的表达式。例如，`Hi (John|Jane)` 匹配 "Hi John" 和 "Hi Jane"。在第 26 行，我们使用字符 `"|"` 来表示地址可以包含一个或多个字符的单词，或一个或多个字符的单词后跟一个空格和另一个一个或多个字符的单词。注意使用括号对正则表达式的各个部分进行分组。量词可以应用于括号中包含的模式，以创建更复杂的正则表达式。

`lastName` 和 `firstName` 变量（第 19 行和第 22 行）都接受以大写字母开头、长度任意的字符串。`address` 字符串的正则表达式（第 26 行）匹配至少一位数字，后跟一个空格，然后是字母一个或多个字符，或者字母一个或多个字符后跟一个空格和另一个一个或多个字母的序列。因此，"10 Broadway" 和 "10 Main Street" 都是有效的地址。按当前构成，第 26 行的正则表达式不匹配不以数字开头或包含超过两个单词的地址。`city`（第 30 行）和 `state`（第 34 行）字符串的正则表达式匹配至少一个字符的任何单词，或者，如果单词由单个空格分隔，则匹配至少一个字符的任意两个单词。这意味着 "Waltham" 和 "West Newton" 都将匹配。同样，这些正则表达式不会接受包含超过两个单词的名称。`zipCode` 字符串的正则表达式（第 37 行）确保邮政编码是五位数字。`phoneNumber` 字符串的正则表达式（第 41 行）表示电话号码必须为 xxx-yyy-yyyy 的形式，其中 x 表示区号，y 表示号码。第一个 x 和第一个 y 不能为零，如每个情况下的范围 `[1-9]` 所指定。

## 21.7.3 替换和拆分字符串

有时很有用将一个字符串的某些部分替换为另一个字符串，或根据正则表达式拆分字符串。为此目的，Boost.Regex 库提供了算法 `regex_replace` 和 `regex_token_iterator` 类，我们在图 21.5 中演示。

算法 `regex_replace` 在字符串中用新文本替换与正则表达式匹配的文本。在第 23 行，`regex_replace` 用 `"A"` 替换 `testString1` 中每个 `"*"` 的实例。请注意，正则表达式（`"\*"`）在字符 `"*"` 前加上反斜杠 `\`。通常，`*` 是一个量词，表示正则表达式应匹配前一个模式的任意次数出现。然而，在这种情况下，我们希望找到字面字符 `"*"` 的所有出现；为此，我们必须用字符 `"\ "` 转义字符 `"*"`。通过用 `\` 转义特殊正则表达式字符，我们告诉正则表达式匹配引擎查找实际字符 `"*"` 而不是将其用作量词。第 27–28 行使用 `regex_replace` 替换字符串
