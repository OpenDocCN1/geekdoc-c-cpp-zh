
```csharp
{
    return anniversary;
}
set {
    if (value.Length > 0) // 我们有字符串吗？
        anniversary = value;
        if (anniversary.Length > DATESIZES) {
            anniversary = anniversary.Substring(0, DATESIZES);
        }
        if (anniversary == null) {
            anniversary = "n/a";
        }
    }
}
public int Status
{
    get {
        return status;
    }
    set {
        if (value == 1) // 激活
            status = value;
        }
        else {
            status = 0; // 非激活
        }
    }
}
public string FileName
{
    get {
        return fileName;
    }
    set {
        if (value.Length > 0)
            fileName = value;
    }
}
public FileStream MyFile
```

```csharp
{
get {
    return myFile;
}
set {
    myFile = value;
}}
```

```csharp
public BinaryReader BinReader {
get {
    return br;
}
set {
    br = value;
}}
```

```csharp
public BinaryWriter BinWriter {
get {
    return bw;
}
set {
    bw = value;
}}
```

```csharp
public String ErrorText {
get {
    return errorMessage;
}}

#endregion

// 普通方法
**** 创建随机访问文件。
* 参数列表：
* 用于文件名的字符串
* 返回值：
* 如果错误返回 0，否则返回 1
*/
public int Create(String fn)
{
    try {
        myFile = new FileStream(fn, FileMode.OpenOrCreate);
        bw = new BinaryWriter(myFile);
        fileName = fn;
    } catch {
        return 0;
    }
    return 1;
}
/**
 打开文件进行读取
* 参数列表：
* 文件名
* 返回值：
* 如果错误返回 0，否则返回 1
*/
public int Open(string fn)
{
    if (bw == null) {
        return Create(fn);
    } else {
        myFile = new FileStream(fn, FileMode.OpenOrCreate);
    }
    return 1;
}
/**
 关闭当前打开的文件。
* 参数列表：
* 无
* 返回值：
* void
*/
public void Close()

# 列表 13-6（续）

```csharp

{

  if (myFile != null)

    myFile.Close();

  if (bw != null)

    bw.Close();

  if (br != null)

    br.Close();

}

/**

 向当前打开的文件写入一条记录

* 参数列表：

* 包含记录号的整数

* 返回值：

* 如果错误返回 0，否则返回 1

* 注意：此方法假设属性包含了

* 要写入的记录。

*/

public int writeOneRecord(long num)

{

  int errorFlag = 1;

  try

{

    if (myFile != null && bw != null)

      // 定位文件指针

      myFile.Seek(num * RECORDSIZE, SeekOrigin.Begin);

      bw = new BinaryWriter(myFile);

    bw.Write(firstName);

    bw.Write(middleInitial);

    bw.Write(lastName);

    bw.Write(address1);

    bw.Write(address2);

    bw.Write(city);

    bw.Write(status);

    bw.Write(zip);

    bw.Write(homePhone);

    bw.Write(cellPhone);

    bw.Write(workPhone);

    bw.Write(email);

    bw.Write(birthday);

    bw.Write(anniversary);

    bw.Write(status);

    bw.Close();

  }

  catch (IOException ex)

  {

    errorMessage = ex.Message; // 以防他们查看。

    errorFlag = 0;

  }

  return errorFlag;

}

/**

 读取一条记录并以字符串形式返回

* 参数列表：

* 包含记录号的整数

* 返回值：

* 如果错误返回 0，否则返回 1

*/

public int ReadOneRecord(long num)

{

try

{

if(myFile != null)

    myFile.Close();

myFile = new FileStream(fileName, FileMode.Open);

br = new BinaryReader(myFile);

if(myFile != null && br != null)

{

// 定位指针

File.Seek(num * RECORDSIZE, SeekOrigin.Begin);

firstName = br.ReadLine();

middleInitial = br.ReadLine();

lastName = br.ReadLine();

address1 = br.ReadLine();

address2 = br.ReadLine();

city = br.ReadLine();

state = br.ReadLine();

zip = br.ReadLine();

homePhone = br.ReadLine();

cellPhone = br.ReadLine();

workPhone = br.ReadLine();

email = br.ReadLine();

birthday = br.ReadLine();

anniversary = br.ReadLine();

status = br.ReadInt32();

br.Close();

}

catch (IOException ex)

{

errorMessage = ex.Message;

return 0;

}

}

# 列表 13-6（续）

/**

* 目的：确定文件中当前记录的数量

* 参数列表：

* void

* 返回值：

* long 文件中的字节数

*/

public long getRecordCount()

{

    long records = 0;

    long remainder;

    try {

        if (myFile != null) {

            // 定位文件指针

            records = myFile.Seek(0, SeekOrigin.End);

            Close();

        }

    } catch (IOException ex) {

        // MessageBox.Show("Error: " + ex.Message);

        return 1;

    }

    remainder = records % RECORDSIZE; // 计算记录数

    records = records / RECORDSIZE;

    if (remainder > 0) { // 部分记录？

        records++; // ...将其考虑在内。

    }

    return records;

}

```

这段代码列表看起来很长……嗯……确实如此！但是，它的很大一部分长度由于属性方法的代码，这些代码相当重复。

# 确定记录大小

首要任务是确定存储你的数据所需的记录大小。在列表 13-6 顶部你可以发现这些：

```csharp

// --------------------

const int NAMESIZES = 20;

const int ADDRESSSIZES = 30;

```

# 顺序文件与随机访问文件 | 40

```csharp

const PHONESIZES = 12;

const int EMAILSIZE = 100;

const int DATESIZES = 10;

const int STRINGSFILE = 14;

const int RECORDSIZE = NAMESIZES // 名字

                + 1

                + NAMESIZES // 间字母

                + ADDRESSSIZES * 2 // 姓

                + 2 // 两个

                + 5 // 城市

                + PHONESIZES * 3 // 邮编

                + EMAILSIZE * 2 // 电话号码

                + DATESIZES // 生日

                anniversary

                + sizeof(int)

                STRINGSFILE;

```

## 408 | 第 13 章 使用磁盘数据文件

| 十进制 | ASCII | 十进制 |
| :--- | :--- | :--- |
| 00000000 00 49 73 79 71 43 05 53 6D 6D 69 74 68 0F 36 35 | [Lucy Smith 65] | 4515 |
| 0000010 37 20 64 69 6E 67 20 65 72 72 65 74 64 65 63 30 | 7 Main Street n/ | |
| 0000020 61 69 61 74 65 72 72 65 74 64 65 73 34 33 33 31 | 657 Springfield, GA 02136 | |
| 0000030 0C 37 20 63 32 36 32 33 35 35 35 35 35 35 33 30 | 706-234-5557 | |
| 0000040 1B 67 69 6C 20 73 6D 6D 69 74 20 69 70 6F 77 79 | lucy.smith@gmail.com | |
| 0000050 72 65 68 69 74 20 74 68 65 64 61 74 62 65 61 31 | A-10-1949 n/a | |

图 13-1: 字符串长度字节

00000 04 49 73 79 71 43 05 53 6D 6D 69 74 68 0F 36 35 (十六进制)
I s s y C S m i t h 6 5 (ASCII)
4 5 15 (十进制)

注意每个字符串前面的二进制值。数字 4 紧跟 Issy 之前，5 紧在 Smith 之前，65 代表 657 Main Street。为什么……难道每个字符串中的数字是告诉我们存储该字符串需要多少个字节吗？是的。

当你在二进制文件中存储字符串时，低层 I/O 代码需要知道每个段字符串数据关联了多少字节。在系统编程中，在二进制文件中存储字符串所需的信息要复杂一些，被称为字符串描述符块。在 C# 中，字符串描述符块简单地称为长度字节。每个字符串都有一个长度，而文件中有 14 个字符串，你需要在计算总记录大时考虑这些长度字节——因此，在记录大小计算的末尾有 STRINGSFILE（因为有 14 个字符串）。

如果你将一个朋友记录中所有数据的字节相加，你会发现 RECORDSIZE 等于 302 字节。因此，在记录写入文件后，文件的外观将类似于图 13-7 所示。

## 写入记录

当用户想要保存记录时，点击 frmMain 中的 Save 按钮。这会导致调用以下方法：

```csharp

recs = myData.GetRecordCount();

myData.Open(TESTDATAFILE);

myData.WriteOneRecord(recs);

```

`getRecordCount()` 中的代码使用 `Seek` 方法将文件指针置到 EOF 尾。当文件指针到达该位置时，它返回当前位置的字节数（作为 `long` 类型）。如果你将文件中的字节数除以其记录大小，就会得到已写入文件的记录数。然而，你需要精炼计算，以考虑到最后一条记录中可能存在“信息间隙”的情况。（参考图 13-8。）如果是如此，记录计数器必须加 1。

接下来，打开数据文件并代码调用 `WriteOneRecord()`，传递用于新文件的记录位置 (recs)。`WriteOneRecord()` 的代码非常直观：

```csharp

public int WriteOneRecord(long num)

{

    int errorFlag = 1;

    try {

        if (myFile != null) {

            // 定位文件

            myFile.Seek(num, SeekOrigin.Begin);

            bw = new BinaryWriter(myFile); // 写入数据

            bw.write(firstName);

            bw.write(middleInitial);

            bw.write(lastName);

            bw.write(address);

            bw.write(city);

            bw.write(state);

            bw.write(zip);

            bw.write(homePhone);

            bw.write(cellPhone);

            bw.write(email);

            bw.write(birthday);

            bw.write(status);

            bw.Close();

        }

    } catch (IOException ex) {

        errorMessage = ex.Message;

        errorFlag = 0;

    }

    return errorFlag;

}

```

## 读取记录

读取的顺序必须与写入顺序匹配。如果读取数据类型出错，文件将立即关闭。理解此程序的最佳方法是单步执行读取和写入。代码所示：

```csharp

public int ReadRecord(long num)

{

    int errorFlag = 1;

    try {

        if (myFile != null) {

            // 定位文件

            myFile.Seek(num, SeekOrigin.Begin);

            br = new BinaryReader(myFile); // 读取数据

            firstName = br.ReadString();

            middleInitial = br.ReadString();

            lastName = br.ReadString();

            address = br.ReadString();

            city = br.ReadString();

            state = br.ReadString();

            zip = br.ReadString();

            homePhone = br.ReadString();

            cellPhone = br.ReadString();

            email = br.ReadString();

            birthday = br.ReadString();

            status = br.ReadString();

            br.Close();

        }

    } catch (IOException ex) {

        errorMessage = ex.Message;
