
下面的代码删除第一个和第二个元素——也就是 `begin()` 和 `begin() + 1` 所指向的元素：

```
scores.erase(scores.begin(), scores.begin() + 2);
```

（由于 vector 提供随机访问，因此像 `begin() + 2` 这样的操作是为 vector 类迭代器定义的。）如果 it1 和 it2 是两个迭代器，STL 文献使用记号 [p1, p2) 来表示一个从 p1 开始、一直到但不包括 p2 的范围。因此，范围 [begin(), end()) 包含集合的全部内容（见图 16.3）。另外，范围 [p1, p1) 为空。（`[)` 记号不是 C++ 的一部分，所以它不会出现在代码中；它只出现在文档中。）

![](img/9afc44517b591d64e2e19f623c9308ef_997_0.png)

图 16.3　STL 范围概念。

> **注意**
> 范围 [it1, it2) 由两个迭代器 it1 和 it2 指定，它从 it1 开始，一直到但不包括 it2。

`insert()` 方法与 `erase()` 方法互补。它接受三个迭代器参数。第一个参数给出一个位置，新元素将插入到该位置之前。第二个和第三个迭代器参数定义要插入的范围。这个范围通常是另一个容器对象的一部分。例如，下面的代码把 new_v 向量中除第一个元素之外的所有元素插入到 old_v 向量的第一个元素之前：

```
vector<int> old_v;
vector<int> new_v;
...
old_v.insert(old_v.begin(), new_v.begin() + 1, new_v.end());
```

顺便说一句，这种情况下有一个尾后元素会很方便，因为它使向 vector 末尾追加内容变得简单。在这段代码中，新内容被插入到 old_v.end() 之前，这意味着它被放在该向量的最后一个元素之后：

```
old_v.insert(old_v.end(), new_v.begin() + 1, new_v.end());
```

程序清单 16.8 演示了 size()、begin()、end()、push_back()、erase() 和 insert() 的用法。为了简化数据处理，程序清单 16.7 中的评分和书名部分被合并到一个 Review 结构中，而 FillReview() 和 ShowReview() 函数为 Review 对象提供输入和输出功能。

### 程序清单 16.8 vect2.cpp

```cpp
// vect2.cpp -- methods and iterators
#include <iostream>
#include <string>
#include <vector>

struct Review {
    std::string title;
    int rating;
};
bool FillReview(Review & rr);
void ShowReview(const Review & rr);

int main()
{
    using std::cout;
    using std::vector;
    vector<Review> books;
    Review temp;
    while (FillReview(temp))
        books.push_back(temp);
    int num = books.size();
    if (num > 0)
    {
        cout << "Thank you. You entered the following:\n"
             << "Rating\tBook\n";
        for (int i = 0; i < num; i++)
            ShowReview(books[i]);
        cout << "Reprising:\n"
             << "Rating\tBook\n";
        vector<Review>::iterator pr;
        for (pr = books.begin(); pr != books.end(); pr++)
            ShowReview(*pr);
        vector<Review> oldlist(books);     // copy constructor used
        if (num > 3)
        {
            // remove 2 items
            books.erase(books.begin() + 1, books.begin() + 3);
            cout << "After erase:\n";
            for (pr = books.begin(); pr != books.end(); pr++)
                ShowReview(*pr);

            // insert 1 item
            books.insert(books.begin(), oldlist.begin() + 1,
                         oldlist.begin() + 2);

            cout << "After insertion:\n";
            for (pr = books.begin(); pr != books.end(); pr++)
                ShowReview(*pr);
        }
        books.swap(oldlist);
        cout << "Swapping oldlist with books:\n";
        for (pr = books.begin(); pr != books.end(); pr++)
            ShowReview(*pr);
    }
    else
        cout << "Nothing entered, nothing gained.\n";
    return 0;
}

bool FillReview(Review & rr)
{
    std::cout << "Enter book title (quit to quit): ";
    std::getline(std::cin, rr.title);
    if (rr.title == "quit")
        return false;
    std::cout << "Enter book rating: ";
    std::cin >> rr.rating;
    if (!std::cin)
        return false;
    // get rid of rest of input line
    while (std::cin.get() != '\n')
        continue;
    return true;
}

void ShowReview(const Review & rr)
{
    std::cout << rr.rating << "\t" << rr.title << std::endl;
}
```

下面是程序清单 16.8 中程序的一次示例运行：

```text
Enter book title (quit to quit): The Cat Who Knew Vectors
Enter book rating: 5
Enter book title (quit to quit): Candid Canines
Enter book rating: 7
Enter book title (quit to quit): Warriors of Wonk
Enter book rating: 4
Enter book title (quit to quit): Quantum Manners
Enter book rating: 8
Enter book title (quit to quit): quit
Thank you. You entered the following:
Rating  Book
5        The Cat Who Knew Vectors
7        Candid Canines
4        Warriors of Wonk
8        Quantum Manners
Reprising:
Rating  Book
5        The Cat Who Knew Vectors
7        Candid Canines
4        Warriors of Wonk
8        Quantum Manners
After erasure:
5        The Cat Who Knew Vectors
8        Quantum Manners
After insertion:
7        Candid Canines
5        The Cat Who Knew Vectors
8        Quantum Manners
Swapping oldlist with books:
5        The Cat Who Knew Vectors
7        Candid Canines
4        Warriors of Wonk
8        Quantum Manners
```

## vector 的更多操作

程序员经常对数组做许多事情，例如搜索、排序、随机打乱顺序等等。vector 模板类有用于这些常见操作的方法吗？没有！STL 采取了更宽泛的视角，为这些操作定义了*非成员*函数。因此，它没有为每个容器类分别定义一个 `find()` 成员函数，而是定义一个可用于所有容器类的 `find()` 非成员函数。这种设计哲学节省了大量重复工作。例如，假设你有 8 个容器类和 10 个要支持的操作。如果每个类都有自己的成员函数，你就需要 8×10，也就是 80 个独立的成员函数定义。但采用 STL 的方式，你只需要 10 个独立的非成员函数定义。而且，如果你定义了一个新的容器类，只要遵循适当的准则，它也可以使用现有的 10 个非成员函数来查找、排序等等。

另一方面，STL 有时会定义一个成员函数，即使它也为同一任务定义了一个非成员函数。原因在于，对于某些操作，存在一种特定于类的算法，它比更通用的算法更高效。因此，vector 的 `swap()` 会比非成员的 `swap()` 更高效。另一方面，非成员版本允许你在两种不同类型的容器之间交换内容。

让我们考察三个有代表性的 STL 函数：`for_each()`、`random_shuffle()` 和 `sort()`。`for_each()` 函数可用于任何容器类。它接受三个参数。前两个参数是定义容器中一个范围的迭代器，最后一个参数是指向函数的指针。（更一般地说，最后一个参数是函数对象；你很快就会学习函数对象。）然后，`for_each()` 函数将所指向的函数应用于该范围内的每个容器元素。所指向的函数不得改变容器元素的值。你可以使用 `for_each()` 函数来代替 `for` 循环。例如，你可以把下面的代码

```
vector<Review>::iterator pr;
for (pr = books.begin(); pr != books.end(); pr++)
    ShowReview(*pr);
```

替换为以下代码：

```
for_each(books.begin(), books.end(), ShowReview);
```

这样你就不必显式使用迭代器变量，避免把手（和代码）弄脏。

`random_shuffle()` 函数接受两个指定范围的迭代器，并以随机顺序重新排列该范围内的元素。例如，下面的语句随机重新排列 books 向量中所有元素的顺序：

```
random_shuffle(books.begin(), books.end());
```

与可用于任何容器类的 `for_each` 不同，这个函数要求容器类允许随机访问，而 vector 类允许随机访问。

`sort()` 函数同样要求容器支持随机访问。它有两个版本。第一个版本接受两个定义范围的迭代器，并使用为容器中存储的元素类型定义的 `<` 运算符对该范围进行排序。例如，下面的代码使用内置的 `<` 运算符比较值，将 `coolstuff` 的内容按升序排序：

```
vector<int> coolstuff;
...
sort(coolstuff.begin(), coolstuff.end());
```

如果容器元素是用户定义的对象，那么为了使用 `sort()`，必须定义一个能用于该类型对象的 `operator<()` 函数。例如，如果你为 `operator<()` 提供了 `Review` 成员函数或非成员函数，就可以对包含 `Review` 对象的 vector 进行排序。由于 Review 是一个结构，其成员是公有的，因此像下面这样的非成员函数就可以满足要求：

```cpp
bool operator<(const Review & r1, const Review & r2)
{
    if (r1.title < r2.title)
        return true;
```
