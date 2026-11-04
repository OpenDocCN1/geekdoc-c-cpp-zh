
## 示例 4.37. 返回指针的函数。

```csharp
using System;

namespace Chapter4 {
    class Class1 {
        static unsafe void Main() {
            int variable;
            int* pointer = &variable;

            Console.WriteLine("Enter a number: ");
            variable = int.Parse(Console.ReadLine());
            pointer = function1(variable, pointer);

            Console.WriteLine("\n {0}", variable);
            pointer = function2(variable, *pointer);

            Console.WriteLine("\n {0}", variable);
            Console.WriteLine("\n {0}", function3(pointer));
        }

        // These first two functions return pointers.
        static unsafe int *function1(int variable, int *pointer) {
            *pointer = variable*(*pointer);
            return (pointer);
        }

        // This function returns a variable.
        static unsafe int *function2(int *pointer, int variable) {
            *pointer = variable / (*pointer);
            return (pointer);
        }

        static unsafe int function3(int *point) {
            return (*point = 20);
        }
    }
}
```

## 存储类说明符：extern 和 static

C# 提供了两个存储类说明符——extern 和 static。第一个存储类说明符 extern，是 external 的缩写，主要用于跨越文件之间移动所造成的限制。该关键字主要用于传递全局引用，并且通常是对象数据类型（结构和类也是如此）。

静态变量是特殊的局部变量，在其函数终止时不会被物理丢弃，而是被存储并在被重新调用时再次应用于这些函数。在许多实际情况下，这种额外的灵活性变得很重要，并且有助于我们消除对全局变量的进一步需求。

## 字符串基础

数组和指针背后的原理应该表明，字符可以组合起来，其总和远不止各部分之和。这种集合的一个简单用途就是简单地组成一个句子，例如：

```c
char array[] = {'T', 'h', 'i', 's', ' ', 'i', 's', ' ', 'a', ' ',
                't', 'h', 'e', ' ', 's', 'i', 'm', 'p', 'l', 'e', 's', 't',
                'a', 'r', 'r', 'a', 'y', ' ', 'o', 'f', ' ', 'd', 'a', 't', 'a',
                's', ' ', 'a', 'n', 'd', ' ', 'a', 'r', 'r', 'a', 'y', 's'};
```

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_285_0.png)

一个稍微不那么明显的选择是将该字符串作为字符数组包含，即“ This is a string of data.” 当然，我们已经看到这两种情况都可以用作输出（Console.Write (String1) 和 Console.Write (Array1[index]);）。然而，想到修改这些过程以包含参数传递和/或存储数据的能力可能就不那么明显了。

字面字符集合，或字符串，可以使用与标准数组相同的方式传递给函数。此字符串参数需要一个已定义的形参（正式称为字符串参数），其等同于数组的参数。字符串将用引号列出，例如，MyString（“This is a string of data”）。字面字符串将作为字符串值存储：static void MyString (string String1) {/* our string function */}。此外，由于字符串与数组处理字面常量不同，我们在尝试添加包含空白字符的字符时不会遭受自动截断的影响。这也应提醒我们 C++ 中使用的 getline 函数，如 cin.getline (array, array_size)，其中我们能够避免此类截断。

### 操作字符串数据

操作字符串数据的另一个重要方面来自 *string extensions* 的使用。这些是包含在基类库中的方法，使许多旧的字符串操作过时。一些基本引用包括测试、更改并应用于字符串及其字面对应物的命令。这些字符串操作符的使用已通过 C（"string.h"）和 C++（"cstring"）传播，这些新定义的方法提供了迄今为止最清晰的表示（见表 4.1）。

**表 4.1.** C#、C++ 和 C 中的字符串数据操作。

| C# | C++ | C |
| :--- | :--- | :--- |
| **复制原始字符串的值到新字符串** | | |
| using System;<br>namespace Chapter4<br>{class Class1<br>{static void Main()<br>{string S = "This is a string\n",<br>S1, S2;<br>S1 = S;<br>S2 = string.Copy(S);<br>Console.WriteLine("{0}\n{1}",<br>S1, S2); } } | #include &lt;iostream&gt;<br>#include &lt;string&gt;<br>using namespace std;<br>void main(void)<br>{string S("This is a<br>string\n"), S1, S2;<br>S1 = S;<br>S2.assign(S);<br>std::cout << S1 <<<br>std::endl<br><< S2 << std::endl; } | #include &lt;iostream&gt;<br>#include &lt;string&gt;<br>using namespace std;<br>void main(void)<br>{char S[] = "This is a string\n",<br>*S1;<br>S1 =<br>(char*)malloc(strlen(S)+1);<br>strcpy(S1, S);<br>std::cout << S1; } |
| **将较长字符串的有限部分复制到较短字符串** | | |
| using System;<br>namespace Chapter4<br>{class Class1<br>{static void Main()<br>{string S = "This is a string\n", S1;<br>S1 = S.Substring(0, 4);<br>Console.WriteLine("{0}", S1); } } | #include &lt;iostream&gt;<br>#include &lt;string&gt;<br>using namespace std;<br>void main(void)<br>{string S("This is a<br>string\n"), S1;<br>S1.assign(S, 0, 4);<br>std::cout << S1 <<<br>std::endl; } | #include &lt;iostream&gt;<br>#include &lt;cstring&gt;<br>using namespace std;<br>void main(void)<br>{char S[] = "This is a string of<br>data\n", S1[] = " ";<br>strncpy(S1, S, 3);<br>std::cout << S1 << std::endl; } |
| **将原始字符串附加额外字符串** | | |
| using System;<br>namespace Chapter4<br>{class Class1<br>{static void Main()<br>{string S = "This is a string\n",<br>Extra = "Good bye";<br>S = S.Insert(17, Extra);<br>Console.WriteLine("{0}", S); } } | #include &lt;iostream&gt;<br>#include &lt;string&gt;<br>using namespace std;<br>void main(void)<br>{string<br>S("This is a string\n"),<br>Extra("Good Bye\n");<br>S.append(Extra); | #include &lt;iostream&gt;<br>#include &lt;cstring&gt;<br>using namespace std;<br>void main(void)<br>{char S[50] = "This is a string<br>of data\n", Extra[] = "Good Bye\n";<br>strcat(S, Extra); |
| **将原始字符串附加额外字符串的有限部分** | | |
| using System;<br>namespace Chapter4<br>{<br>class Class1<br>{static void Main()<br>{string S = "This is a string\n";<br>Extra = "Good bye";<br>S = S.Insert(17, Extra.Substring(0,4));<br>Console.WriteLine("{0}", S); } } | #include &lt;iostream&gt;<br>#include &lt;string&gt;<br>using namespace std;<br>void main(void)<br>{string S("This is a string\n");<br>Extra("Good Bye\n");<br>S.append(Extra, 0, 4);<br>std::cout << S <<<br>std::endl; }<br>其中 0 是起始点，4 是附加的长度。 | #include &lt;iostream&gt;<br>#include &lt;cstring&gt;<br>using namespace std;<br>void main(void)<br>{char OurArray[50] = "This is a string of data\n";<br>Extra[] = "Good Bye\n This string is too long and would cause an error.";<br>strncat(OurArray, Extra, 10);<br>std::cout << OurArray <<<br>std::endl; } |
| **比较两个字符串** | | |
| using System;<br>namespace Chapter4<br>{class Class1<br>{static void Main()<br>{string S = "This is a string\n";<br>Extra = "Good bye";<br>if(Extra.CompareTo(S) == 0)<br>Console.WriteLine("They match!");<br>else<br>Console.WriteLine("They don't match!");<br>if(string.Equals(S, S))<br>Console.WriteLine("Found!");<br>if(string.ReferenceEquals(S, S))<br>Console.WriteLine("Found!"); } } } | #include &lt;iostream&gt;<br>#include &lt;string&gt;<br>using namespace std;<br>void main(void)<br>{string S("This is a string\n");<br>S1("This is a string\n");<br>S2("Is this string larger?\n");<br>if(S == S1)<br>std::cout <<<br>"I can't tell them a part\n";<br>int test =<br>S1.compare(S2);<br>if(test == 0) std::cout <<<br>"There equal";<br>else if(test > 0) std::cout<br><< "S2 is greater";<br>else if(test < 0) std::cout<br><< "S1 is greater";<br>std::cout << std::endl; } | #include &lt;iostream&gt;<br>#include &lt;cstring&gt;<br>using namespace std;<br>void main(void)<br>{char S[] = "This is a string\n";<br>char S1[] = "This is a string\n";<br>char S2[] = "Is this string larger?\n";<br>if(!(strcmp(S, S1)))<br>std::cout <<<br>"I can't tell them a part\n";<br>if(strcmp(S, S2) > 0) // T > S<br>std::cout <<<br>"I think I was cheated \n"; } |
| **比较字符串1的有限部分与字符串2** | | |
| using System;<br>namespace Chapter4<br>{class Class1<br>{static void Main()<br>{string S = "This is a string\n"; | #include &lt;iostream&gt;<br>#include &lt;string&gt;<br>using namespace std;<br>void main(void)<br>{int T; | #include &lt;iostream&gt;<br>#include &lt;cstring&gt;<br>using namespace std;<br>void main(void)<br>{char S1[] = "This is a string\n", |
