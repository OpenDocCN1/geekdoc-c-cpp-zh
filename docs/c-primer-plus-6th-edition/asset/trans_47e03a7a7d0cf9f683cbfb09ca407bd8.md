
输入书籍评分：8

输入书名（输入 quit 退出）：quit
谢谢。你输入了以下内容：

评分 书名

+ 5 懂向量的猫
7 诚实的犬类
4 Wonk 上的战士们
8 量子礼仪

重新列出：

评分 书名

+ 5 懂向量的猫
7 诚实的犬类
4 Wonk 上的战士们
8 量子礼仪

删除后：

+ 5 懂向量的猫
8 量子礼仪

插入后：

+ 7 诚实的犬类
5 懂向量的猫
8 量子礼仪

将旧列表 oldlist 与 books 交换：

+ 5 诚实的犬类
7 Wonk 上的战士们
8 量子礼仪

# 向量还需要做的更多事情

许多程序员通常会对数组执行这些操作，例如搜索、排序、随机化顺序等。不！STL（标准模板库）有着更全面的视角，为这些操作定义了非成员函数。它没有为每个容器定义单独的 `find()` 成员函数，而是定义了一个适用于所有容器的单一 `find()` 成员函数。这种设计哲学解决了大量的重复工作。例如，假设你有 8 个容器类和需要支持的10 个操作。如果每个类都有自己的成员函数，你需要编写 8x10（即 80）个独立的成员函数定义。但使用 STL 的方法，你只需要 10 个非成员函数定义。如果你定义了一个新的容器类，只要它遵循适当的指南，就可以使用现有的 10 个非成员函数进行查找、排序等操作。

另一方面，STL 有时即使为同一任务定义了非成员函数，也会定义一个成员函数。这是因为对于某些操作，特定于类的算法比通用的算法更高效。因此，`vector` 的 `swap()` 会比非成员的 `swap()` 更高效。另一方面，非成员版本允许你在两个不同类型的容器之间交换内容。

让我们检查三个代表性的 STL 函数：`for_each()`、`random_shuffle()` 和 `sort()`。`for_each()` 函数可以用于任何容器类。它接受三个参数：前两个是定义容器中范围的迭代器，最后一个是指向函数的指针。（更泛地说，最后一个是函数对象；你很快就会学到函数对象。）`for_each()` 函数随后应用所指向的函数，该函数不能修改容器元素的值。你可以使用 `for_each()` 函数代替循环。例如，你可以将以下代码：

```
vector<Review>::iterator pr;
for (pr = books.begin(); pr != books.end(); pr++)
    ShowReview(*pr);
```

替换为以下内容：
`for_each(books.begin(), books.end(), ShowReview);`

这让你能够避免因显式使用迭代器变量而让手（以及代码）感到疲劳。

`random_shuffle()` 函数接受两个迭代器来指定范围，并随机顺序重新排列该范围内的元素。例如，以下语句将重新排列 `books` 向量中所有元素的顺序：
`random_shuffle(books.begin(), books.end());`

不同与适用于任何容器的 `for_each` 不同，此函数要求容器类允许随机访问，而 `vector` 是支持的。
`sort()` 函数同样要求容器支持随机访问。它有两个版本。第一个版本接受两个迭代器来定义范围，并使用存储在容器中的元素类型定义的 `<` 运算符对该范围进行排序。例如，以下代码使用内置的 `<` 运算符比较值，对 `coolstuff` 的内容进行升序排序：

```
vector<int> coolstuff;
...
sort(coolstuff.begin(), coolstuff.end());
```

如果容器元素是用户定义的对象，那么必须为该类型的对象定义一个 `operator()` 函数才能使用 `sort()`。例如，如果你提供一个 `Review` 成员函数或非成员函数，就可以对包含 `Review` 对象的向量进行排序（注：这里应为 `operator<`）。例如，如果你提供一个 `Review` 成员函数或非成员函数，就可以对包含 `Review` 对象的向量进行排序：

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>

using namespace std;

struct Review {
    string title;
    int rating;
};

bool operator<(const Review& r1, const Review& r2)
{
    if (r1.title < r2.title)
        return true;
    else if (r1.title == r2.title && r1.rating < r2.rating)
        return true;
    else
        return false;
}

bool WorseThan(const Review& r1, const Review& r2)
{
    if (r1.rating < r2.rating)
        return true;
    else
        return false;
}

void ShowReview(const Review & rr)
{
    cout << rr.rating << "\t" << rr.title << endl;
}

bool FillReview(Review & rr)
{
    cout << "Enter book title (quit to quit): ";
    getline(cin,rr.title);
    if (rr.title == "quit")
        return false;
    cout << "Enter book rating: ";
    cin >> rr.rating;
    if (!cin)
        return false;
    // 丢掉输入行的剩余部分
    while (cin.get() != '\n')
        continue;
    return true;
}

int main()
{
    vector<Review> books;
    Review temp;
    while (FillReview(temp)) {
        books.push_back(temp);
    }

    if (books.size() > 0) {
        cout << "You entered the following:\n";
        for_each(books.begin(), books.end(), ShowReview);

        cout << "Sorted by title:\n";
        sort(books.begin(), books.end());
        for_each(books.begin(), books.end(), ShowReview);

        cout << "Sorted by rating:\n";
        sort(books.begin(), books.end(), WorseThan);
        for_each(books.begin(), books.end(), ShowReview);

        cout << "After shuffling:\n";
        random_shuffle(books.begin(), books.end());
        for_each(books.begin(), books.end(), ShowReview);
    } else {
        cout << "No entries.\n";
    }
    cout << "Bye.\n";
    return 0;
}
```

这是 Listing 16.9 程序的示例运行：

输入书名（输入 quit 退出）：The Cat Who Can Teach You Weight Loss
输入评分：8
输入书名（输入 quit 退出）：The Dogs of Dhara
输入评分：6
输入书名（输入 quit 退出）：The Wimps of Wonk
输入评分：3
ter书名（输入 quit 退出）：Farewell and Delete
输入评分：7

