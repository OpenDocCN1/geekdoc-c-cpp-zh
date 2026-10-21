

```cpp
++i;
}
cout << "The size of StudMarks is " << StudMarks.size() << endl;
vector <Student>::iterator index;
sort(StudMarks.begin(), StudMarks.end());
for(index = StudMarks.begin(); index < StudMarks.end(); ++index)
    cout << *index << endl;
}
```

### 程序的工作原理

我们可以用内置类型以及用户自定义类型作为向量的元素。对所有容器都适用。

让我们尝试理解这个程序。Student 类也在本程序中使用。需要注意的是，类中已经定义了运算符 `=` 和 `<` 以及 `<<` 运算符。`sort()` 算法需要 `<` 运算符被重载。

下面的语句定义了一个向量 StudMarks，其中包含 Student 对象。

```cpp
vector <Student> StudMarks;
```

然后，有一个 for 循环，它读取每个学生的成绩，然后使用 push_back 将其插入向量中。

成员函数 `size()` 已被用来查找向量的大小，即向量中元素的数量。因此，下面的语句显示了向量中元素的数量。

```cpp
cout << "The size of StudMarks is " << StudMarks.size() << endl;
```

下一个语句为 `vector <Student>` 定义了一个迭代器 index。这里调用了通用算法 `sort()`。

```cpp
sort(StudMarks.begin(), StudMarks.end());
```

该算法只需要两个参数；两者都是随机访问迭代器的类型。这种排序算法是原地排序算法。它对传递给它的同一个向量进行排序。向量范围再次以 `[first, last)` 提供，其中包括第一个和最后一个之间的所有元素，包括第一个但不包括最后一个。

接下来使用与前面类似的 for 循环进行 Student 数据的打印。

前面已经提到，向量可以动态增长。程序 16.3 说明了这一特性。函数 `capacity()` 返回向量在不增长的情况下可以容纳的元素数量。

### 程序 16.3 增长的向量

```cpp
//GrowingVector.cpp
#include <vector>
#include <iostream>
#include <string>
using namespace std;

class Student
{
    int RollNumber;
    string Name;
public:
    Student(int TempRollNumber, string TempName)
    {
        RollNumber = TempRollNumber;
        Name = TempName;
    }
};

int main()
{
    vector <Student> vs;
    vector <int> vi;
    cout << "The capacity of the Student vector is " << vs.capacity() << endl;
    cout << "The capacity of the integer vector is " << vi.capacity() << endl;
    int TempSizeInt = vi.capacity();
    int TempSizeStudent = vs.capacity();

    for(int i = 0; i < 200; i++)
    {
        vi.push_back(i);
        if(vi.capacity() != TempSizeInt)
        {
            cout << "The capacity of the vector changes to " << vi.capacity() << endl;
            TempSizeInt = vi.capacity();
        }
    }

    Student Lara(1, "Brian Charles Lara");

    for(int i = 0; i < 200; i++)
    {
        vs.push_back(Lara);
        if(vs.capacity() != TempSizeStudent)
        {
            cout << "The capacity of the vector changes to " << vs.capacity() << endl;
            TempSizeStudent = vs.capacity();
        }
    }
}
```

**Output (in VC++ 7.0)**

```text
The capacity of the Student vector is 0
The capacity of the integer vector is 0
The capacity of the vector changes to 1
The capacity of the vector changes to 2
The capacity of the vector changes to 3
The capacity of the vector changes to 4
The capacity of the vector changes to 6
The capacity of the vector changes to 9
The capacity of the vector changes to 13
The capacity of the vector changes to 19
The capacity of the vector changes to 28
The capacity of the vector changes to 42
The capacity of the vector changes to 63
The capacity of the vector changes to 94
The capacity of the vector changes to 141
The capacity of the vector changes to 211
// Student vector output
The capacity of the vector changes to 1
The capacity of the vector changes to 2
The capacity of the vector changes to 3
The capacity of the vector changes to 4
The capacity of the vector changes to 6
The capacity of the vector changes to 9
The capacity of the vector changes to 13
The capacity of the vector changes to 19
The capacity of the vector changes to 28
The capacity of the vector changes to 42
The capacity of the vector changes to 63
The capacity of the vector changes to 94
The capacity of the vector changes to 141
The capacity of the vector changes to 211
```

Linux 的输出如下：

```text
The capacity of the Student vector is 0
The capacity of the integer vector is 0
The capacity of the vector changes to 1
The capacity of the vector changes to 2
The capacity of the vector changes to 4
The capacity of the vector changes to 8
The capacity of the vector changes to 16
The capacity of the vector changes to 32
The capacity of the vector changes to 64
The capacity of the vector changes to 128
The capacity of the vector changes to 256

// Student vector output
The capacity of the vector changes to 1
The capacity of the vector changes to 2
The capacity of the vector changes to 4
The capacity of the vector changes to 8
The capacity of the vector changes to 16
The capacity of the vector changes to 32
The capacity of the vector changes to 64
The capacity of the vector changes to 128
The capacity of the vector changes to 256
```

### 程序的工作原理

让我们尝试理解这个程序及其输出。它有一个 Student 向量和一个 int 向量，类似于程序 16.1。`vi.capacity()` 和 `vs.capacity()` 已被用来查找两个向量的容量，并且整数 TempSizeInt 用于计算它们的容量。程序使用 `vi.push_back(i)` 在 int 向量 `vi` 中插入一个 int 对象，并使用 `vs.push_back(Lara)` 在 Student 向量 `vs` 中插入一个 Student 对象。如果向量的当前容量与之前的容量不同，则显示新的容量。然后，它继续在两种情况下向向量中添加 200 个元素。

现在，看看程序在测试过的两个不同编译器上产生的输出。第一个编译器是 VC++ 7.0。这里的向量增长是任意的。Linux 编译器的输出要直接得多。每次向量填满时，其大小都会加倍。注意，对于内置类型或用户自定义类，增长是相似的。对于大型类对象可能会有所不同。

当向量已满并且尝试插入时，向量的容量会增加。它会自动管理增长。向量增长的方式取决于特定的编译器。

## 16.6.2 列表

列表是下一个容器类型，它是双向链表的模板化实现。在学习了第一个容器之后，学习另一个容器很容易，因为操作容器的方式相当相似。让我们看一个例子，其中向量被列表取代，除了一个地方。程序 16.4 打印成绩单，现在使用列表而不是向量。

### 程序 16.4 STL 列表对象

```cpp
//MeritList.cpp
#include <iostream>
#include <list>
#include <algorithm>
using namespace std;

class Student
{
private:
    int RollNumber;
    float TotalMarks;
public:
    Student(){};
    Student(int TempRollNumber, float TempTotalMarks)
    {
        RollNumber = TempRollNumber;
        TotalMarks = TempTotalMarks;
    }

    void operator = (Student TempStud)
    {
        RollNumber = TempStud.RollNumber;
        TotalMarks = TempStud.TotalMarks;
    }

    bool operator < (Student TempStud)
    {
        return(TotalMarks < TempStud.TotalMarks);
    }
    friend ostream & operator <<(ostream & TempOut, Student & TempStud);
};

ostream & operator <<(ostream & TempOut, Student & TempStud)
{
    TempOut << "The mark of roll number " << TempStud.RollNumber << " is " << TempStud.TotalMarks;
    return TempOut;
}

void main()
{
    list <Student> StudMarks;
    float TempMarks;
    int i = 0;
    for(;;)
    {
        cout << "Enter mark for roll number " << i + 1 << " Enter -1 to stop: ";
        cin >> TempMarks;
        if(TempMarks == -1) break;
        StudMarks.push_back(Student(i + 1, TempMarks));
        ++i;
    }
}
```
