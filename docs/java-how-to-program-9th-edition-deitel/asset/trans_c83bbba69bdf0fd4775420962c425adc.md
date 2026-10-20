

文件中的记录。问题在于文本文件中的字段（从而记录）大小可能不同。例如，7、14、−117、2074 和 27383 都是 int，在内部以相同的字节数（4）存储，但当显示在屏幕上或作为文本写入文件时，它们却是大小不同的字段。因此，顺序访问文件中的记录通常不会就地更新，而是通常重写整个文件。要进行上述姓名更改，300 Pam White 0.00 之前的记录会被复制到新文件中，然后写入新记录（其大小可能与所替换的记录不同），再将 300 Pam White 0.00 之后的记录复制到新文件中。只为更新一条记录而重写整个文件并不经济，但如果需要更新大量记录，则是合理的。

## 17.5 对象序列化

在 17.4 节中，我们演示了如何将 AccountRecord 对象的各个字段作为文本写入文件，以及如何从文件读取这些字段并将其值放入内存中的 AccountRecord 对象。在示例中，AccountRecord 用于聚合一条记录的信息。当 AccountRecord 的实例变量输出到磁盘文件时，某些信息会丢失，例如每个值的类型。例如，如果从文件中读取值“3”，则无法判断它是来自 int、String 还是 double。磁盘上只有数据，没有类型信息。如果将要读取该数据的程序“知道”数据对应的对象类型，那么数据就会被简单地读入该类型的对象中。例如，在 17.4.2 节中，我们知道输入的是一个 int（账号），后跟两个 String（名字和姓氏）和一个 double（余额）。我们还知道这些值以空格分隔，每行只有一条记录。有时我们并不确切知道数据在文件中的存储方式。在这种情况下，我们希望从文件读取或写入整个对象。Java 提供了这样一种机制，称为对象序列化。所谓序列化对象，是指将对象表示为一个字节序列，其中包含对象的数据以及有关对象类型和对象中存储数据类型的信息。序列化对象写入文件后，可以从文件中读取并进行反序列化——即，可以使用表示对象及其数据的类型信息和字节在内存中重新创建对象。

> 软件工程观察 17.1
> 序列化机制可以制作对象的精确副本。这提供了一种简单的克隆对象的方法，而无需覆盖 Object 的 clone 方法。

## ObjectInputStream 和 ObjectOutputStream 类

ObjectInputStream 和 ObjectOutputStream 类分别实现了 ObjectInput 和 ObjectOutput 接口，支持从流（可能是文件）中读取整个对象或将整个对象写入流。为了将序列化用于文件，我们使用读写文件的流对象（分别是 FileInputStream 和 FileOutputStream 类的对象）来初始化 ObjectInputStream 和 ObjectOutputStream 对象。以这种方式用其他流对象初始化流对象有时称为包装——正在创建的新流对象包装了作为构造器参数指定的流对象。例如，要将 FileInputStream 包装在 ObjectInputStream 中，我们将 FileInputStream 对象传递给 ObjectInputStream 的构造器。

## ObjectOutput 和 ObjectInput 接口

ObjectOutput 接口包含 writeObject 方法，该方法接收一个 Object 作为参数，并将其信息写入 OutputStream。实现 ObjectOutput 接口的类（如 ObjectOutputStream）声明了此方法，并确保输出的对象实现 Serializable 接口（稍后讨论）。相应地，ObjectInput 接口包含 readObject 方法，该方法从 InputStream 读取并返回一个 Object 的引用。读取对象后，可以将其引用转换为对象的实际类型。正如你将在第 27 章中看到的，通过网络（如 Internet）通信的应用程序也可以跨网络传输整个对象。

## 17.5.1 使用对象序列化创建顺序访问文件

本节和 17.5.2 节将使用对象序列化创建和操作顺序访问文件。我们在此展示的对象序列化是使用基于字节的流执行的，因此创建和操作的文件将是二进制文件。回想一下，二进制文件通常无法在标准文本编辑器中查看。因此，我们编写一个单独的应用程序，它知道如何读取和显示序列化对象。我们首先创建序列化对象并将其写入顺序访问文件。该示例与 17.4 节中的示例类似，因此我们只关注新特性。

## 定义 AccountRecordSerializable 类

首先修改 AccountRecord 类，使该类的对象可以被序列化。AccountRecordSerializable 类（图 17.15）实现了 Serializable 接口（第 7 行），该接口允许 AccountRecordSerializable 对象分别使用 ObjectOutputStream 和 ObjectInputStream 进行序列化和反序列化。Serializable 接口是一个标记接口（tagging interface）。这种接口不包含方法。实现 Serializable 的类被标记为可序列化对象。这一点很重要，因为 ObjectOutputStream 不会输出对象，除非它是 Serializable 对象，而实现 Serializable 的类的任何对象都是如此。

```
// Fig. 17.15: AccountRecordSerializable.java
// AccountRecordSerializable class for serializable objects.
package com.deitel.ch17; // packaged for reuse

import java.io.Serializable;

public class AccountRecordSerializable implements Serializable
{
    private int account;
    private String firstName;
    private String lastName;
    private double balance;
    
    // no-argument constructor calls other constructor with default values
    public AccountRecordSerializable()
    {
        this(0, "", "", 0.0);
    } // end no-argument AccountRecordSerializable constructor
```

```
72      // get balance
73      public double getBalance()
74      {
75          return balance;
76      } // end method getBalance
77  } // end class AccountRecordSerializable
```

### 图 17.15 | 用于可序列化对象的 AccountRecordSerializable 类。（第 3 部分，共 3 部分。）

在 Serializable 类中，每个实例变量都必须是 Serializable 的。非 Serializable 的实例变量必须声明为 transient，以表明在序列化过程中应忽略它们。默认情况下，所有基本类型变量都是可序列化的。对于引用类型变量，必须查看类的文档（可能还有其超类）以确保该类型是 Serializable 的。例如，String 是可序列化的。默认情况下，数组是可序列化的；但在引用类型数组中，被引用的对象可能不是可序列化的。AccountRecordSerializable 类包含私有数据成员 account、firstName、lastName 和 balance——它们都是 Serializable 的。该类还提供了用于访问私有字段的公有 get 和 set 方法。

## 将序列化对象写入顺序访问文件

现在讨论创建顺序访问文件的代码（图 17.16–17.17）。这里我们只关注新概念。如 17.2 节所述，程序可以通过创建流类 FileInputStream 或 FileOutputStream 的对象来打开文件。在本示例中，文件将以输出方式打开，因此程序创建了一个 FileOutputStream（图 17.16 的第 21 行）。传递给 FileOutputStream 构造器的 String 参数表示要打开的文件的名称和路径。以这种方式为输出而打开的现有文件会被截断。我们为包含序列化对象的二进制文件选择了 .ser 文件扩展名，但这不是必需的。

> 常见编程错误 17.2
> 当你实际上希望保留现有文件时，以输出方式打开它是一个逻辑错误。FileOutputStream 类提供了一个重载构造器，使你可以打开文件并将数据追加到文件末尾。这样可以保留文件的内容。

```
// Fig. 17.16: CreateSequentialFile.java
// Writing objects sequentially to a file with class ObjectOutputStream.
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectOutputStream;
import java.util.NoSuchElementException;
import java.util.Scanner;

import com.deitel.ch17.AccountRecordSerializable;

public class CreateSequentialFile
{
    private ObjectOutputStream output; // outputs data to file
```

### 图 17.16 | 使用 ObjectOutputStream 创建的顺序文件。（第 1 部分，共 3 部分。）

