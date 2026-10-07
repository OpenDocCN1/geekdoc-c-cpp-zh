
```java
import java.io.*;

public class Program9 {

  public static void main(String args[]) {

    StringBuilder str=new StringBuilder("hello");

    System.out.println(str.reverse());

  }

}
```

Ans. 程序将打印：
olleh

### Q10. 执行以下程序时你会得到什么输出？

```java
public class Program10 {
  public static void main(String args[]) {
    String org = "this";
    String search = "is";
    String sub = "was";
    String result = "";
    int i=org.length();
    for(int j=0;j<i;j++) {
      result = org.substring(0, j);
      result = result + sub;
      result = result + org.substring(j + search.length());
      org = result;
    }
    System.out.println(org);
  }
}
```

Ans. 程序将打印：
Wwwawisis

- 程序

- Q1. 写一个程序，帮助我们理解如何创建字符串以及如何使用 `String` 类的一些重要方法。

// String 类方法的演示

```java
class StrDemo
{
  public static void main(String args[]) {
  }
}
```

## 字符串处理 205

// 三种方式创建字符串
`String s1 = "A book on Java";`
`String s2 = new String("I like it");`
`char[] arr = {'c', 'p', 'r', 'a', 'm', 't', 'e', 'c', 'h', 'n', 'p', 'r', 'e', 's', 's'};`
`String s3 = new String(arr);`
// 显示所有字符串
`System.out.println(s1);`
`System.out.println(s2);`
`System.out.println(s3);`
// 第一个字符串的长度
`System.out.println("Length of " + s1);`
// 拼接两个字符串
`System.out.println("s1 and s2 joined " + s1);`
// 拼接三个字符串
`System.out.println("from " + s3);`
// 测试 s1 是否以 A 开头
`boolean x = s1.startsWith("A");`
`if(x) else System.out.println("s1 does not start with A");`
// 提取 s2 从第 0 个到第 6 个字符的内容
`String p = s2.substring(0,7);`
// 提取 s3 从第 0 个到第 8 个字符的内容
`String q = s3.substring(0,9);`
// 拼接字符串 p 和 q
`System.out.println(p+q);`

输出:
A book on Java
I like it
Dreamtech Press
Length of s1=14
s1 and s2 joined A book on Java
A book on Java from Dreamtech
s1 starts with "A"
I like

2. 写一个程序，使用 `String` 类创建一个字符串并反序显示字符串。

```java
class Program2 {
    public static void main(String args[]) {
        String str=new String("Hello Java");
        int len=str.length();
        for(int x=len-1; x>=0; x--) {
            System.out.print("" + str.charAt(x));
        }
    }
}
```

输出:
a v a J olle H

3. 写一个程序，使用 `String` 类创建一个字符串并检查该字符串是否为回文。回文是指正读反读都相同的单词或句子。

```java
class Program3 {
    public static void main(String args[]) {
        String s="radar";
        int c=s.length();
        boolean flag=false;
        for(int x=0,y=c-1; x<c/2; x++, y--) {
            if(s.charAt(x)==s.charAt(y)) {
                flag=true;
            } else {
                flag=false;
            }
        }
        if(flag==true) {
            System.out.println("The string " + s + " is a palindrome");
        } else {
            System.out.println("The string " + s + " is not a palindrome");
        }
    }
}
```

输出:
The string radar is a palindrome

4. 写一个程序，使用 `String` 类创建一个字符串并检查该字符串是否为回文。回文是指正读反读都相同的单词或句子。

```java
class Program4 {
    public static void main(String args[]) {
        String org = "this";
        String search = "is";
        String sub = "was";
        String result = "";
        int i=org.length();
        for(int j=0;j<i;j++) {
          result = org.substring(0, j);
          result = result + sub;
          result = result + org.substring(j + search.length());
          org = result;
        }
        System.out.println(org);
    }
}
```

输出:
Wwwawisis

204 ► 第 6 章

### Q5. 执行以下程序时你会得到什么输出？

```java
class StrCompare
{
    public static void main(String args[])
    {
        String s1="hello";
        String s2="Hello";
        if(s1==s2)
            System.out.println("Both are same");
        else System.out.println("Not same");
    }
}
```

Ans. 程序将打印：
Both are same

### Q6. 执行以下程序时你会得到什么输出？

```java
public class Program6
{
    public static void main(String args[])
    {
        String str = "Excellent";
        for(int x=0;x<str.length; x++)
            System.out.println(str);
    }
}
```

Ans. 程序无法编译，因为应该使用 `str.length()` 方法来获取长度，而不是 `str.length`。

### Q7. 执行以下程序时你会得到什么输出？

```java
public class Program7
{
    public static void main(String args[])
    {
        String str = "Excellent";
        System.out.println(str.replace('t', ' '));
    }
}
```

Ans. 程序将打印：
Excellen.

### Q8. 执行以下程序时你会得到什么输出？

```java
public class Program8
{
    public static void main(String args[])
    {
        String str1=new String("Hello");
        String str2=new String("Hello");
        int x=5;
        if(str1.equals(str2))
        {
          System.out.println("true 1");
          if(str==x) {
            System.out.println("true 2");
          }
        }
    }
}
```

Ans. 程序无法编译，因为字符串值与整型值进行了比较。

### Q9. 执行以下程序时你会得到什么输出？

```java
import java.io.*;

public class Program9 {
  public static void main(String args[]) {
    StringBuilder str=new StringBuilder("hello");
    System.out.println(str.reverse());
  }
}
```

Ans. 程序将打印：
olleh

### Q10. 执行以下程序时你会得到什么输出？

```java
public class Program10 {
  public static void main(String args[]) {
    String org = "this";
    String search = "is";
    String sub = "was";
    String result = "";
    int i=org.length();
    for(int j=0;j<i;j++) {
      result = org.substring(0, j);
      result = result + sub;
      result = result + org.substring(j + search.length());
      org = result;
    }
    System.out.println(org);
  }
}
```

Ans. 程序将打印：
Wwwawisis

# 210 第 7 章

例如，在编写一个除以两个数字的方法时，程序员可能编写了将数字除以 0 的代码，这是不允许的。将数字除以 0 不会导致编译错误，但它会导致程序在执行过程中中断。当找不到文件或存在内存相关问题（如栈溢出）时，程序可能会被中断。列表 1 声明了 `DemoException` 类，用来说解释程序执行过程中可能发生的异常（你可以在第7章文件夹的 CD 中找到 `DemoException.java` 文件）：

- 列表 1：显示 `DemoException.java`

```java
package com.kogent;

class DemoException {
    public static void main (String[] args) {
        int x=5;
        int y=0;
        int z=x/y;
        System.out.println("Result of the program is " + z);
    }
}
```
