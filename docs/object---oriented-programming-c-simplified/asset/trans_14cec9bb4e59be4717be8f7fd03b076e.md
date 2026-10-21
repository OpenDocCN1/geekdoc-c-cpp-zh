

```
file.read((char*)&d,sizeof(d));
 d.show( );
 file.close( );
 getch( );
}
```

# 输出：

姓名 = HARI
年龄 = 24

# 说明：

write 和 read 这两个函数用于处理二进制文件。首先，我们使用函数 input 为对象 d 的数据成员赋值。然后调用函数 write，其第一个参数是对象 d 的地址，即执行写入的位置，第二个参数是对象的大小。将对象写入文件后，通过 read 函数进行读取，其语法与 write 类似。读取对象后，通过调用函数 show 进行显示。

# /* 程序 12.25 读写对象 版本 2 */

```
#include <iostream.h>
#include <fstream.h>
#include <string.h>
#include <conio.h>

class person
{
    char name[10];
    int age;
    char sex;
public :
    void input()
    {
        cout<<"Enter person name"<<endl;
        cin>>name;
        cout<<"Enter age and sex"<<endl;
        cin>>age>>sex;
    }
    void show()
    {
        cout<<"Name :-"<<name<<endl;
        cout<<"Age :-"<<age<<endl;
```

```
cout<<"Sex :="<<sex<<endl;
}
};
void main()
{
    fstream file;
    file.open("obj.txt",ios ::in|ios ::out);
    person d[3];
    int i;
    clrscr();
    for(i=0;i<3;i++)
    {
        d[i].input();
        file.write((char*)&d[i],sizeof(d[i]));
    }
    cout<<"Data read from file"<<endl;
    for(i=0;i<3;i++)
    {
        cout<<"\n Person"<<i+1<<"\n";
        file.read((char*)&d[i],sizeof(d[i]));
        d[i].show();
    }
    file.close();
}
```

# 输出：

输入人名
HARI
输入年龄和性别
24 m
输入人名
MAN
输入年龄和性别
26 M
输入人名
RANJANA
输入年龄和性别
23 F

```
Data read from file
Person1
Name := HARI
Age := 24
Sex := m
Person2
Name := MAN
Age := 26
Sex := M
Person3
Name := RANJANA
Age := 23
Sex := F
```

说明：在程序中，我们有一个大小为 3 的 person 类对象数组 d。我们运行 for 循环，并使用函数 input 为所有三个对象的数据成员取值。然后使用函数 read 将对象存储到文件中。在下一个 for 循环中，我们从文件中读取对象并使用 write 进行显示。

# /* 程序 12.26 读写数组 */

```
#include <iostream.h>
#include <fstream.h>
#include <conio.h>

void main()
{
    fstream file;
    int a[10], i;

    clrscr();

    file.open("arr.txt",ios :: in|ios :: out);
    for(i=0;i <=9;i++)
        a[i]=i+1;
    file.write((char*)a,sizeof(a));
    cout << "Array is" << endl;
    for(i=0;i <=9;i++)
        cout << endl << " " << a[i];
    cout << endl;
```

```
long int move;
clrscr( );
file.open("student.txt",ios :: in|ios :: out|ios :: binary
    |ios :: ate);

do
{
    cout << "\n Welcome to student Database\n";
    cout << "1. Add a record\n";
    cout << "2. View Record \n";
    cout << "3. Search Record \n";
    cout << "4. Delete a Record \n";
    cout << "5. Modify a record \n";
    cout << "6. Count Records \n";
    cout << "7. Exit\n";
    cout << "Enter your choice (1 to 6)\n";
    cin >> ch;
    switch(ch)
    {
    case 1 :st.input_data( );
        file.write((char*)&st, sizeof(st));
        cout << "Record is added \n";
        file.clear( );
        break;
    case 2 : file.seekg(0,ios :: beg);
        while(file.read((char*)&st, sizeof(st)))
            st.show_data( );
        file.clear( );
        break;
    case 3 :cout << "Enter the college roll number \n";
        cin >> crn;
        file.seekg(0,ios :: beg);
        while(file.read((char*)&st,sizeof(st)))
        {
            if(st.getcrn( ) == crn)
            {
                cout << "Record found\n";
                st.show_data( );
                found = 1;
            }
        }
        if(found == 0)
```

```
cout << "Record does not found \n";
file.clear();
break;
case 4 :cout << "Enter the college roll number \n";
cin >> crn;
file.seekg(0,ios ::beg);
while(file.read((char*)&st,sizeof(st)))
{
if(st.getcrn() == crn)
{
cout << "Record found \n";
found =1;
st.show_data();
int ans;
cout << "Are you sure to delete this
record (1/0) ?\n";
cin >> ans;
if(ans == 1)
{
file.seekg(0,ios ::beg);
fstream newf;
newf.open("newstu.txt",ios ::out);
while(file.read((char*)&st,sizeof(st)))
{
if(st.getcrn() != crn)
newf.write((char*)&st,sizeof(st));
}
file.close();
remove("student.txt");
newf.close();
rename("newstu.txt","student.txt");
file.open("student",ios ::in|ios ::out|ios ::binary
|ios ::ate);
cout << "Record deleted\n";
}
}
}
if(found == 0)
cout << "Record does not found\n";
file.clear();
break;
```

## Hilbert空间上复合算子的性质研究

曹广福 何莉

摘要  本文研究解析函数空间上复合算子的若干性质。设 φ 为解析自映射，定义复合算子 C_φf = f∘φ。本文讨论了 C_φ 的有界性、紧性及谱性质，并给出了相关判定条件。

关键词  复合算子；函数空间；Hilbert空间；紧性；谱

### 1 引言

设 H 是区域 Ω 上的解析函数构成的 Hilbert 空间，φ: Ω → Ω 是解析自映射。复合算子 C_φ 定义为 C_φ(f) = f(φ(z))。近年来，复合算子的研究引起了广泛关注，其在动力系统、函数论及算子理论中均有重要应用。

本文的主要目的是研究 C_φ 在若干解析函数空间上的有界性与紧性。我们首先介绍相关预备知识，然后给出主要定理及其证明。

### 2 预备知识

定义 2.1  设 H 为 Hilbert 函数空间，其再生核为 K_w(z)。若对任意 w ∈ Ω，K_w ∈ H 且满足 f(w) = ⟨f, K_w⟩，则称 H 为再生核 Hilbert 空间。

引理 2.2  若复合算子 C_φ 在 H 上有界，则对任意 w ∈ Ω，有 K_w / ‖K_w‖ 在 C_φ 的作用下有界。

### 3 主要结论

定理 3.1  设 φ 为 Ω 上的解析自映射，则 C_φ 在 H 上有界当且仅当存在常数 M > 0，使得对任意 w ∈ Ω，有 ‖C_φ*K_w‖ ≤ M‖K_w‖。

定理 3.2  若 φ 在 Ω 内无界轨道，则 C_φ 非常值且为下有界算子。

证明  利用上述引理及算子理论中的标准方法，可得结论成立。∎

### 参考文献

- 1. Cowen C C, MacCluer B D. Composition Operators on Spaces of Analytic Functions. CRC Press, 1995.
- 2. Shapiro J H. Composition Operators and Classical Function Theory. Springer, 1993.
- 3. Zhu K. Operator Theory in Function Spaces. American Mathematical Society, 2007.

```
Welcome to student Database
1. Add a record
2. View Record
3. Search Record
4. Delete a Record
5. Modify a record
6. Count Records
7. Exit
Enter your choice (1 to 6)
1
Enter the student name
Ravi
Enter college roll no and class
13 MBA
Record is added
Welcome to student Database
1. Add a record
2. View Record
3. Search Record
4. Delete a Record
5. Modify a record
6. Count Records
7. Exit
Enter your choice (1 to 6)
2
Name := Hari        CRN := 12 Class := B Tech
Name := Ravi        CRN := 13 Class := MBA
Welcome to student Database
1. Add a record
2. View Record
3. Search Record
4. Delete a Record
5. Modify a record
6. Count Records
7. Exit
Enter your choice (1 to 6)
Welcome to student Database
1. Add a record
2. View Record
3. Search Record
4. Delete a Record
```

```
5. Modify a record
6. Count Records
7. Exit
Enter your choice (1 to 6)
7
Bye Bye
```

# 说明：

要修改一条记录，我们首先定位到该记录的位置。该位置可按如下方式计算：

```
Loc=(n-1) *sizeof(st);
```

其中 st 是 student 类的对象，n 是记录编号。

然后通过 seekg 到达文件中的该位置，即待修改记录的开头。接着我们接收该记录的新数据，并覆盖现有记录。

文件以 ios :: ate 模式打开，该模式将指针置于文件末尾。要在文件中任意移动，我们必须使用 seekg。一旦设置了文件末尾标志，为了再次访问文件，我们使用 clear 函数将其清除，该函数会关闭文件末尾标志。

要搜索一条记录，我们向用户询问学院编号，并扫描整个文件以查找 c_rno 与用户提供的 crn 相匹配的记录。由于 c_rno 是私有的，所以我们有一个公共成员函数 getcrn 来获取学院编号。

要删除一条记录，我们将所有其他记录移动到一个临时文件 temp.txt。然后使用内置函数 remove 删除原始文件，该函数接受一个 const char* 类型的参数，即要删除的文件名。然后我们将临时文件 temp.txt 重命名为原来的 student.txt。

# 12.9 错误处理

处理文件时可能会发生错误，例如：

- 文件不存在
- 从仅以写入模式打开的文件中进行读取。
- 路径无效。
- 文件已存在等。

为了应对所有这些错误，我们会检查文件是否成功打开，或者产生了什么类型的错误。

下面给出一些错误处理函数及其说明：

# 1. good 函数

```
SYNTAX : int good( ) const;
```

如果所有错误位均已清除，则返回非零值。注意，good 成员函数并不是 bad 函数的简单逆函数。

# 2. bad 函数

```
SYNTAX : int bad( ) const;
```

