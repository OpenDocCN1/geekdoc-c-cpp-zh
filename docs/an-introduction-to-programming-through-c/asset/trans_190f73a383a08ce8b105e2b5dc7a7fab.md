
编写此程序的自然方式是使用一个结构体来读取学号和分数。然后我们会使用一个结构体向量。为了能够对结构体向量进行排序，我们只需定义一个成员函数 `operator<`，它决定在给定两个结构体时哪个结构体应被视为更小。由于我们希望按学号排序，我们必须将包含较小数值的结构体视为较小的结构体。这正是下面代码中 `operator<` 的定义所做的事情。请注意一个重要之处：`sort` 函数要求定义 `operator<` 函数，并且接收者和参数都必须是 `const`。

```
struct student{
    int rollno;
    float marks;
    bool operator<(const student& rhs) const{ // used by the sort function
        return rollno < rhs.rollno;             // note the two const keywords
    }
};

int main(){
    vector<student> svec;

    student s;
    while(cin >> s.rollno){
        cin >> s.marks;
        svec.push_back(s);
    }

    sort(svec.begin(), svec.end());             // will use operator< internally

    for(int i=0; i<svec.size(); i++)
        cout << svec[i].rollno << " " << svec[i].marks << endl;
}
```

## 20.4.3 成绩显示变体 3

假设现在的输入与第 20.4.2 节相同，但我们想要两种打印输出：一种按学号排序，另一种按分数排序。现在在 `student` 类中定义 `operator<` 已经不够了，我们可以定义它按学号排序，或按分数排序，但不能同时按两者排序。

因此在这种情况下，我们首先定义一个比较函数。例如我们可以定义：

```
bool compareMarksFunction(const student &a, const student &b){
    return a.marks < b.marks;
}
```

稍后我们将看到如何利用它按分数排序。请注意，我们本可以使用函数对象而不是普通函数。为了有所变化，我们将使用函数对象来按学号排序。因此，我们首先定义一个结构体，从中创建函数对象。

```
struct compareRollnoStruct{
    bool operator() (const student& a, const student& b){
        return a.rollno < b.rollno;
    }
};
```

现在可以编写主程序了。

```
int main(){
    // code to define svec and read into it as before
    sort(svec.begin(), svec.end(), compareMarksFunction);    // by marks
    for(unsigned i=0; i<svec.size(); i++)
        cout << svec[i].rollno << " " << svec[i].marks << endl;
    sort(svec.begin(), svec.end(), compareRollnoStruct());    // by roll no
    for(unsigned i=0; i<svec.size(); i++)
        cout << svec[i].rollno << " " << svec[i].marks << endl;
}
```

在这段代码中，两次对 `sort` 的调用都传入了一个额外参数，以指定排序必须如何进行。第一次调用中的参数实际上是一个函数指针，但 `&` 运算符没有写出，因为它可以省略（见第 11.7.1 节）。第二次调用中，最后一个参数是 `compareRollnoStruct()`。这是对构造函数的调用，因此传入的是 `compareRollnoStruct` 类的一个对象。它用于决定排序顺序。

如你所见，向 `sort` 传递函数或函数对象比在类中定义 `operator<` 更灵活——你可以通过传递不同的函数或函数对象，按照不同的顺序进行排序。

## 20.5 map 模板类

理解 `map` 类最简单的方式，是把它看作是数组或向量的泛化。在数组或向量中，如果数组长度为 n，则索引必须是 0 到 n − 1 之间的整数。而在 `map` 中，这一条件被大大放宽：你可以使用任何值作为索引，甚至不必是数值！与数组一样，索引的值决定了所引用的是 `map` 中的哪个元素。

要使用 `map` 模板类，你需要包含头文件 `<map>`。接下来，声明你想要的 `map`。

```
map<indexType,valueType> mapname;
```

这将创建一个名为 `mapname` 的 `map`。它存储 `valueType` 类型的元素，可以通过提供 `indexType` 类型的索引来访问。要求为 `indexType` 类型定义 `operator<`。当然，如果该运算符原本没有定义，你可以定义它。不过，该定义应具备比较运算符通常应有的性质，即它应当是传递的和非对称的。

让我们看一个简单的例子。假设我们要存储不同国家的人口。那么我们可以创建一个名为 `Population` 的 `map`，它将存储人口数值（数字）。假设我们以十亿为单位存储人口，因此我们的 `valueType` 是 `double`。我们希望使用国家名称来访问每个国家对应的元素，因此我们的 `indexType` 可以是 `string`。于是我们可以如下定义我们的 `map`。

```
map<string,double> Population;
```

接下来，我们将想要的信息插入 `map` 中，即指定不同国家的人口。

```
Population["India"] = 1.21; // population of India is 1.21 billion
Population["China"] = 1.35;
Population["United States"] = 0.31;
Population["Indonesia"] = 0.24;
Population["Brazil"] = 0.19;
```

例如，第一行创建了一个值为 `1.21`、索引为 `"India"` 的元素。你也可以使用类似数组访问的语法来引用已创建的元素。例如，下面的代码

```
cout << Population["Indonesia"] << endl;
```

将打印 `0.24`，也就是索引为 `"Indonesia"` 的元素中存储的值。

你必须认识到，虽然这些语句表面上看起来像数组访问，但它们的实现当然会非常不同。实际上，当你编写 `Population["India"] = 1.21;` 时，实际存储的是 `("India",1.21)` 这个对。名称 `Population` 实际上指的是这样一系列对的集合。随后，当我们编写 `Population["India"]` 时，我们实际上是在说：引用第一个元素为 `"India"` 的那个对的第二个元素。因此，需要执行一些代码来找到这个元素（见第 20.5.2 节）。所以当你使用 `map` 时，幕后发生了很多事情。

如果你对同一个索引写两次赋值，例如

```
Population["India"] = 1.21;
Population["India"] = 1.22;
```

这将产生你所期望的效果：第一次创建的元素将被修改，使其存储的值从 `1.21` 变为 `1.22`。

你可能希望对 `map` 执行的一个重要操作是检查该 `map` 是否包含具有给定索引的元素。假设你已将某个国家的名称读入字符串变量 `country`。假设你想打印该国的人口（如果它存在于 `map` 中）；否则，你想打印一条消息，说明该国家的人口不为程序所知。你可以如下编写：

```
cout << "Give the name of the country: ";
string country;
cin >> country;
if (Population.count(country)>0)
    cout << Population[country] << endl;
else cout << country << " not found.\n";
```

这段代码应紧跟在上面定义 `map Population` 并指定各国人口的代码之后。

在这段代码中，成员函数 `count` 以索引值为参数；如果给定 `map` 中存在具有该索引的元素，则返回 1。因此，假设用户在我们要求给出国家名称后键入了 `"India"`，那么 `Population.count(country)` 将返回 1，因为我们之前确实将 `"India"` 的人口输入到了 `map` 中。所以在这种情况下，最终输入的值 `1.22` 将被打印出来。另一方面，如果键入的国家是 `"Britain"`，那么 `Population.count(country)` 将返回 0，因此将打印消息 `"Britain not found."`。另一种确定 `map` 是否包含某个条目的方法将在第 20.6.1 节讨论。

你可能会好奇，如果我们无论如何都要执行下面的语句，会发生什么

```
cout << Population["Britain"] << endl;
```

而在代码中之前没有为 `Population["Britain"]` 赋值。这条语句的执行在某种程度上有些违反直觉。通常，假设我们已经定义了一个 `map`

```
map<X,Y> m;
```

并假设 `x` 是类型 `X` 的一个值。那么，如果我们访问 `m[x]` 而没有先为其赋值，这会隐式地导致首先执行语句 `m[x]=Y();`，即为索引 x 创建一个元素，该元素存储调用类 `Y` 的默认构造函数所获得的值 `Y()`。之后返回 `m[x]` 的值。因此，对于语句 `cout << Population["Britain"] << endl;`，会首先执行语句 `Population["Britain"]=double();`。遗憾的是，类型 `double` 的构造函数不会初始化该值。所以该 `map` 现在将包含一个值未知但索引为 `"Britain"` 的元素。因此，这个未知值将被打印出来。

## 20.5.1 成绩显示变体 4

在本节中，我们将让教师输入学生的姓名而不是学号。我们将考虑最初的问题，即学生走到计算机前想知道自己的分数。但这一次，他们输入的是姓名而不是学号。显然，我们可以使用字符串来表示学生姓名，并使用 `map` 来存储学生的分数。

为了使问题更有趣，我们假设每个学生都有数学、物理和梵文三门课程的成绩。进一步假设姓名在文件中按如下形式给出：

```
A. A. Fair, 85, 95, 80
Vibhavari Shirurkar, 80, 90, 90
Nicolas Bourbaki, 95, 99, 75
```

