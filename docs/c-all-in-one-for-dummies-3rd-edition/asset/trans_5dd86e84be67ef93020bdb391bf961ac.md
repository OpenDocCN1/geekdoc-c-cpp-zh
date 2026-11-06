
下面的列表详细描述了使数组成为常量的规则：

![](img/6ba99460b0feb3585671a4612ff5fabb_456_0.png)

-   如果你想使数组成为常量，可以在其类型前加上 const 一词。这样做时，数组名是常量，数组内的元素也是常量。因此，你不可能拥有元素非常量的常量数组，也不可能拥有元素为常量的非常量数组。
-   非常量数组的概念只存在于 gcc 中，并不是 ANSI 标准。

![](img/6ba99460b0feb3585671a4612ff5fabb_456_1.png)

如果你真的想从技术层面深究，C++ ANSI 标准指出，当你在数组声明前加上 const 一词时，并不是在把数组本身变成常量；你是在说该数组只保存常量。不过，当你这样使用 const 时，大多数编译器也会把数组本身变成常量。但这样没问题；人们不应该取一个数组名并把它复制到别处。这不是良好的编程风格，只会招致 bug——或者至少会在以后造成困惑。

## 用指针指向

要完全理解 C++ 及其所有的怪异与奇妙之处，你需要成为指针专家。最大的 bug 来源之一，是对 C++ 一知半解的程序员使用指针并把它们搞乱的时候。但在这种情况下，糟糕的是，应用程序可能正常运行一段时间，然后突然不工作。这些 bug 是最难捕捉的，因为用户可能看到问题发生，然后报告它；但当程序员试图重现问题时，却无法让这个 bug 发生！（就像你把车送去修理，它却突然不犯毛病了。）修车工和程序员都会说：“我试的时候明明好好的！”这多令人沮丧啊？

在本节中，我们将向你展示如何充分利用指针，并在应用程序中正确使用它们，从而避免这些奇怪的问题。

### 变得极其复杂

这不是我们编的；我们见过这样的函数头：

```c
void MyFunction(char ***) {
```

哎呀！那些星号都是干什么用的？看起来像是指向指针的指针的指针，指向……某个东西！真让人困惑。现在，假设有些人的大脑更像计算机，他们能看着那段代码并完全理解。我们可不行。所以如果你也看不懂，别担心。

| 第 IV 部分 | 第 1 章 |
| --- | --- |
| 使用数组、指针和引用 | |

接下来，我们调用 `MyFunction()`。该函数应该改变指针所指向的内容。然后我们从函数返回并打印两个字符：`ptr` 指向的字符和 `copy` 指向的字符。运行后得到如下结果：

```text
ptr points to B
copy points to A
```

这意味着它成功了！`ptr` 变量现在指向在 `MyFunction` 中分配的字符（一个 B），而 `copy` 变量仍然指向原来的 A。换句话说，它们不再指向同一个东西：`MyFunction()` 成功改变了该变量所指向的内容。

现在考虑同一个函数，但这次不用引用，而是用指针来试。下面是修改后的形式（如 Pointer02 示例所示）：

```cpp
void AnotherFunction(PChar *x)
{
    *x = new char('C');
}
```

现在，因为参数是指针，我们必须解引用它才能修改其值。因此，中间一行开头有一个星号 `*`。

下面是调用该函数的修改后的 `main()`：

```cpp
char *ptr = new char('A');
char *copy = ptr;
AnotherFunction(&ptr);
cout << "ptr points to " << *ptr << endl;
cout << "copy points to " << *copy << endl;
```

因为我们的函数使用指针而不是引用，所以必须传递 `ptr` 变量的地址，而不是直接传递 `ptr` 变量。因此请注意，对 `AnotherFunction()` 的调用在 `ptr` 前面有一个与号 `&`。这段代码按预期工作。运行它时，我们看到以下输出：

```text
ptr points to C
copy points to A
```

这个版本的函数名为 `AnotherFunction()`，它新建了一个名为 C 的字符。确实工作正常：`ptr` 现在指向字符 C，而 `copy` 没有改变。该函数再次让 `ptr` 指向了别的东西。

现在我们可以把这件事理清。我们创建了一个 `typedef`，说实话，我们更愿意把它保留在代码中，因为我们认为使用 `typedef` 能让函数在做什么更容易理解。然而，并不是每个人都那样做；因此，当我们不得不介入并修复别人的代码时，就必须理解其他人在做什么。你可能也不得不这样做。所以下面是同样的两个函数 `MyFunction()` 和 `AnotherFunction()`，但不使用 typedef。它们没有使用新的 PChar 类型，而是直接使用等价的 `char **` 类型：

```c
void MyFunction(char **x)
{
    x = new char ('B');
}
```

```c
void AnotherFunction(char **x)
{
    *x = new char ('C');
}
```

为了去掉对 typedef 的使用，我们所做的只是把两个函数头中的 PChar 替换为等价的 `char **`。你可以看到，这些函数头现在看起来更古怪了。但它们与之前含义完全相同：第一个是指向指针的引用，第二个是指向指针的指针。

但请先想一想 `char ** x`。因为在许多方面，`char *` 也等同于字符数组，所以 `char **x` 是指向字符数组的指针。事实上，有时你可能会看到 `main()` 的头文件写成这样

```c
int main(int argc, char **argv)
```

而不是

```c
int main(int argc, char *argv[])
```

注意，这两者中第一个的 argv 参数与我们一直在谈论的类型相同：指向指针的指针（或者，用更容易理解的方式说，是 PChar 的地址）。但你知道，`main()` 的参数是字符串数组。

所以请耐心跟着这个有点绕的思路走（如果必要就慢慢来）：如果你有一个指向字符串数组的指针，并且有一个函数要让它指向另一个字符串数组，会怎样？

最好给这个也做个 typedef；它会变得很难看。提醒一下，我们仍在使用之前的 typedef，即 PChar（如 Pointer03 示例所示）：

```c
typedef char **StringArray;
typedef char *PChar;
```

前三个是我们传入函数的 `OrigList` 中的元素：但它们不再具有 John、Paul 和 George 这些值。三个最初的披头士名字已被三个新名字取代：Tom、Harry 和 Suzy。然而，`CopyList` 变量仍然指向原来的字符串列表。因此，它又一次成功了。

我们通过引用完成了从 John、Paul 和 George 到 Tom、Harry 和 Suzy 的更改，但也可以用指针做到。下面是该函数的修改版本，这次使用前面所说的指针（如 `Pointer04` 示例所示）：

```cpp
void ChangeAsPointer(StringArray *array)
{
    StringArray NameArray = new PChar[3];
    NameArray[0] = "Tom";
    NameArray[1] = "Harry";
    NameArray[2] = "Suzy";
    *array = NameArray;
}
```

和之前一样，下面是用于测试该函数的稍作修改的示例代码：

```cpp
StringArray OrigList = new PChar[3];
OrigList[0] = "John";
OrigList[1] = "Paul";
OrigList[2] = "George";
StringArray CopyList = OrigList;
ChangeAsPointer(CopyList);
cout << OrigList[0] << endl;
cout << OrigList[1] << endl;
cout << OrigList[2] << endl;
cout << CopyList[1] << endl;
cout << CopyList[2] << endl;
```

你可以看到，当我们调用 `ChangeAsPointer()` 时，传递的是 OrigList 的地址。这个版本的输出与上一个版本相同。

现在，和之前一样，我们把这一切理清。下面是不使用 typedef 的两个函数头：

```c
int ChangeAsReference(char **array) {
```

以及

```c
int ChangeAsPointer(char ***array) {
```
