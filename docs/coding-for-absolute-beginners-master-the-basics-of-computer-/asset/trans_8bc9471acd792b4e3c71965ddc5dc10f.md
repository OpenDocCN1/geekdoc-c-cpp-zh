

```text
"country": "Sweden"
}
```

## 面向对象 Python

在面向对象编程中，我们需要定义类和对象，以在程序中执行各种功能。与 C++ 和 C 等其他主要编程语言一样，我们可以使用面向对象技术来创建、访问和更新类。

要在 Python 中创建学生类，代码编写如下：

```python
class student:
    def __init__(self, roll, name):
        self.r = roll
        self.n = name
        print(self.n)

# ...
stud1 = student(1, "James")
stud2 = student(2, "William")

print("Data successfully stored in variables")
```

访问对象变量时，使用点运算符（.），其语法为：

`object_name.variable_name`

### 继承

继承是面向对象编程的一个有用特性，它允许开发者创建一个新类，以继承现有类的所有方法和属性。我们可以使用继承技术，定义一个具有父类或基类属性的新子类或派生类。

在 Python 中实现继承的语法定义如下：

```python
class BaseClass1:
    #Body of Base Class
class DerivedClass(BaseClass1):
    #body of derived class
```

以下程序展示了 Vehicle 作为父类，以及一个派生类，该派生类将继承父类 Vehicle 的特性并调用其函数。

```python
class Vehicle:  #parent class
    "Parent Class"
    def __init__(self, price):
        self.price = price

    def display(self):
        print ('Price = $',self.price)

class Category(Vehicle):   #derived class
    "Child/Derived class"
    def __init__(self, price, name):
        Vehicle.__init__(self, price)
        self.name = name

    def disp_name(self):
        print ('Vehicle =',self.name)

obj = Category(2000, 'Mercedes')
obj.disp_name()
obj.display()
```

**输出：**

车辆 = Mercedes
价格 = $2000

要重写基类中的任何方法，我们可以在派生类中定义一个具有相同名称和参数的新方法。语法如下：

```python
class A:  #parent class
    "Parent Class"
    def display(self):
        print ('This is base class.')

class B(A):  #derived class
    "Child/Derived class"
    def display(self):
        print ('This is derived class.')

obj = B()
obj.display()
```

## 正则表达式

在 Python 编程中，正则表达式用于从文本中提取信息，包括文档、日志文件、电子表格或代码。正则表达式被称为按特殊顺序排列的字符，允许程序员使用专门语法查找相关序列、字符或字符串集合。每当在 Python 编程语言中编写正则表达式时，我们应该以前缀 ‘r’ 开始原始字符串，以及其他特殊元字符。

### match() 函数

match() 函数用于检查给定正则表达式在 Python 中是否匹配字符串。如果模式不匹配，我们可以使用 re.match() 函数。

### search() 函数

此函数尝试搜索字符串中的所有可能起点，并扫描输入字符串以匹配任何位置。它包括 search() 或 re.search() 函数。

### split() 函数

split 函数可以直接应用于字符串，而 re.split() 接受一个指定分隔符的模式。

## 文件 I/O

文件是磁盘上用于存储信息和数据的特定位置。由于它存储在硬盘中，我们也可以通过实现 Python 编程方法和技术来执行读写操作。Python 中的文件操作包括三个主要方面：打开文件、读取或写入文件，以及关闭文件。

open() 是 Python 编程语言中的内置函数，它有两个参数，称为文件名和模式。可以实现以下方法来在文件中执行不同操作：

- “r” = 打开或读取文件。
- “w” = 写入文件，如果文件不存在则创建新文件。
- “a” = 打开文件以进行追加，如果文件不存在则创建新文件。
- “x” = 创建新文件，如果文件已存在则返回错误。
- “t” = 以文本模式打开。
- “b” = 以二进制模式打开。
- “+” = 打开文件以进行读取或写入。

### 实现这些方法的语法

```python
f = open("sample.txt")
f = open("img.jpg", "r")
```

要关闭文件，我们可以使用 f.close() 函数。

### 在 Python 中读取文件

通过 Python 编程语言读取特定文件很简单，我们可以实现 read(size) 方法。例如：

```python
>>> f = open("Sample.txt",'r')
>>> f.read(4)    # read the first 4 data
'This'
>>> f.read(4)    # read the next 4 data
'is '
>>> f.read()    # read in the rest till end of file
'my first file\nThis file\ncontains four lines\n'
>>> f.read()
```

### 在服务器上打开文件

要使用内置 open() 函数打开文件，我们可以使用以下语法：

```python
f = open("Samplefile.txt", "r")
print(f.read())
```

要读取特定行，我们可以实现 readline() 函数：

```python
f = open("Samplefile.txt", "r")
print(f.readline())
```

### 写入现有文件

以下 Python 编程语法将打开示例文件并追加内容：

```python
f = open("Samplefile.txt", "a")
f.write("Update your content")
f.close()
```

### 追加后打开并读取文件

```python
f = open("Samplefile.txt", "r")
print(f.read())
```

### 创建文件

要创建新文件，将使用 open() 方法，它可以具有创建、追加或写入参数。在 Python 中创建文件的语法定义如下：

```python
f = open("Newfile.txt", "w")
```

### 删除文件

要删除现有文件，应使用 os.remove() 函数，语法如下：

检查文件是否存在的语法。如果存在，则删除它：

```python
import os
os.remove("Samplefile.txt")
if os.path.exists("Samplefile.txt"):
    os.remove("Samplefile.txt")
else:
    print("The file does not exist")
```

## 高级 Python

### 异常处理

Python 编程语言中有三种主要的异常处理方法。try、except 和 finally 块用于处理程序执行期间发生的错误。

#### try

要通过 try 块生成异常，可以实现以下语法：

```python
try:
    print(x)
except:
    print("An exception occurred")
```

如果没有引发错误，示例代码如下：

```python
try:
    print("Python")
except:
    print("An exception occurred")
else:
    print("No exception occurred")
```

#### finally

在异常处理中，即使 try 块是否引发了异常，finally 块都会执行。例如：

```python
try:
    print("Python")
except:
    print("An exception occurred")
finally:
    print("try exception finished")
```

#### 用户自定义异常

尽管 Python 编程语言中有几个内置异常可用于在出现问题时强制程序显示错误，但开发者也可以创建自定义异常以满足其需求。要创建新异常，必须从 Exception 类创建一个新类。

用户自定义异常可以像普通类一样实现，因为大多数内置异常都派生自 Exception 类。

### 学习 Python 的建议

Python 编程语言最适合对人工智能、机器学习、机器人技术或应用开发感兴趣的程序员。在开始编程本身之前，你必须充分了解 Python 基础语法。学习方法、途径和语法将使初学者更容易开始编码并自行开发任何类型的应用程序。

对于初学者来说，进行小型编码练习非常有益。他们可以培养敏锐的解决问题的能力，并利用他们的编程概念。此外，Python 程序或应用程序也可以贡献到开源项目，初学者可以从那里获得关于他们工作的评论和建议。

我还写了一本关于 Python 的书。[Python 零基础入门] 将帮助你在 Python 编程方面打下坚实的基础。

