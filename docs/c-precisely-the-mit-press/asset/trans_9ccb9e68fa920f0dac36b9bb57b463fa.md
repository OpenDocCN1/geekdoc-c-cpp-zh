

# 异步方法：async 和 await (C# 5.0) 143

示例 176 使用 async 和 await 进行异步数据检索
方法 NbiEntQueryAsync 和 NbiProteinAsync 的行为与示例 170 中返回任务的方法相同，但 `async` 和 `await` 关键字提供了更整洁的语法语法。

```csharp
public static async Task<String> NbiEntrezAsync(String query) {
    byte[] bytes = await newClient().DownloadDataAsync(new Uri(server + query));
    return ASCIIICode.GetString(bytes);
}
```

```csharp
public static async Task<String> NbiProteinAsync(String id) {
    return await NbiEntrezAsync("etch.fcgi?retype=fasta&retmode=textdb=proteinid=" + id);
}
```

示例 177 并行异步数据检索
为了检索许多蛋白质，可以使用异步方法 NbiProteinAsync（示例 176）。`from` 表达式为每个蛋白质 ID 创建并启动一个任务，而 `WhenAll` 创建一个任务来等待所有任务完成，收集结果并通过数组返回。

```csharp
public static async Task<String[]> NbiProteinParallelAsync(params String[] ids) {
    IEnumerable<Task<String>> tasks = from id in ids select NbiProteinAsync(id);
    return await Task.WhenAll(tasks);
}
```

示例 178 复合异步数据检索
对 NCBI PubMed Publication数据库的查询必须分两个步骤进行：首先是返回包含 WebEnv 键的 XML 文档的搜索查询；然后是获取实际结果的查询。异步方法执行此类两步查询，调用两次异步方法 NbiEntrezAsync（示例 176）。由于结果是一个任务，可以进一步添加超时处理（示例 179）或使用 `WhenAll` 并行执行许多此类两步查询（示例 177）。

```csharp
public static async Task<String> NbiPubMedAsync(String term) {
    String search = String.Format("etch.fcgi?db=PubMed&retmode=l&term={0}", term);
    XmlDocument xml = new XmlDocument();
    xml.LoadXml(await NbiEntrezAsync(search));
    XmlNode node = xml["EsearchResult"];
    String fetch = String.Format("retmax=3&db=PubMed&query_key={0}&WebEnv={1}", node["Query"].InnerText, node["WebEnv"].InnerText);
    return await NbiEntrezAsync("etch.fcgi?retype=abstract&retmode=text" + fetch);
}
```

示例 179 使用 async 和 await 实现超时
可以使用异步方法和 `await` 实现超时（示例 173）。

```csharp
public static async Task<double> SlowTimeout2Task(int n) {
    Task<double> slowFibTask = SlowFibTask(n);
    Task completed = await Task.WhenAny(slowFibTask, Task.Delay(1000));
    return completed == slowFibTask ? slowFibTask.Result : -1;
}
```

![](img/0895719d2f186cd73b49fccec3a97f1f_155_0.png)

# 数学函数

## 24 数学函数

Math 类提供了静态方法来计算数学函数。浮点数（double 和 float）遵循 IEEE754 标准，包括正无穷和负无穷大作为非数字，称为 NaN。此外，正零和负零之间也有区别，在此处予以忽略。

这些方法在应用于非法参数时会返回非数字（NaN），在发生溢出时返回无穷大；不会抛出异常。当应用于正无穷或负无穷大时，它们的行为是合理的；如果存在极限则返回该极限，否则返回 NaN。在出现相等的情况下，这些方法将舍入到最近的偶整数。Abs 和 Sign 方法针对 float、int、long、byte 和 short 类型的参数进行了重载；Min 和 Max 方法针对无符号类型进行了重载。

- * static double E 是数 e≈2.71828，自然对数的底数。
- * static double PI 是常数 π≈3.14159，直径为 1 的圆的周长。
- * static double Abs(double x) 是绝对值：如果 x<0，则返回 -x。
- * static double Acos(double x) 是 x 的反余弦，范围在 [0,π] 之间，适用于 -1<=x<=1。
- * static double Asin(double x) 是 x 的反正弦，范围在 [-π/2,π/2] 之间，适用于 -1<=x<=1。
- * static double Atan(double y, double x) 是 y/x 在 (x, y) 象限内的反正正切，范围在 [-π,π] 之间。当 x 为 0 时，结果为 π/2，符号与 y 相同。
- * static double Ceil(double x) 是>=x 的最小整数。
- * static double Cos(double x) 是 x 的余弦，范围在 [-1,1] 之间。
- * static double Exp(double x) 是 x 的指数，即 e 的次方。
- * static double Floor(double x) 是<=x 的最大整数。
- * static double IEEERemainder(double x, double y) 是 x/y 的余数，即 x-y，最接近 x/y。当 x 为负且 y 为正时，结果可能为负。
- * static double Log(double x) 是 e 的对数，适用于 x>=0。
- * static double Log10(double x) 是10为底的对数，适用于 x>0。
- * static double Min(double x, double y) 是 x 和 y 中的最小值。
- * static double Pow(double x, double y) 是 x 的 y 次方，x^y。如果 y 为 1，结果为 x。如果 y 为 0，结果为 1。
- * static double Round(double x) 是最接近 x 的整数。
- * static double Sin(double x) 是 x 的正弦。
- * static int Sign(double x) 返回 +1、0 或 -1。
- * static double Sqrt(double x) 是 x 的平方根，适用于 x>=0。
- * static double Tan(double x) 是 x 的正切。

# 示例 180 浮点阶乘
该方法使用对数计算 $n! = 1 \cdot 2 \cdot 3 \cdots (n-1) \cdot n$。

```csharp
static double Fact(int n) {
    double res = 0.0;
    for (int i=1; i<n; i++)
        res += Math.Log(i);
    return Math.Exp(res);
}
```

# 示例 181 生成伪随机数
此示例使用 Box-Muller 变换生成均值为 0、标准差为 1 的高斯分布随机数。

```csharp
Random rnd = new Random();
for (int i=0; i<n; i++) {
    double x1 = rnd.NextDouble(), x2 = rnd.NextDouble();
    Print(Math.Sqrt(-2 * Math.Log(x1)) * Math.Cos(2 * Math.PI * x2));
    Print(Math.Sqrt(-2 * Math.Log(x1)) * Math.Sin(2 * Math.PI * x2));
}
```

# 示例 182 数学函数：无穷大、NaN 和特殊情况
```csharp
Print("非法参数，NaN结果:");
Print(Math.Sqrt(-1)); // NaN
Print(Math.Log(-1)); // NaN
Print(Math.Pow(-1, 2.5)); // NaN
Print(Math.Acos(1.1)); // NaN
Print("无穷结果:");
Print(Math.Log(0)); // -Infinity
Print(Math.Pow(0, -1)); // -Infinity
Print(Math.Exp(1000.0)); // Infinity (溢出)
Print("无穷参数:");
double infinity = Double.PositiveInfinity;
Print(Math.Sqrt(infinity)); // Infinity
Print(Math.Log(infinity)); // Infinity
Print(Math.Pow(infinity, -1)); // 0
Print(Math.Pow(infinity, 0.5)); // Infinity
Print(Math.Pow(0.5, infinity)); // 0
Print(Math.Pow(0.5, -infinity)); // Infinity
Print(Math.Pow(2, infinity)); // Infinity
Print("特殊情况:");
Print(Math.Pow(0, 0)); // 1.0
Print(Math.Pow(infinity, 0)); // 1.0
Print(Math.Pow(-infinity, 0)); // 1.0
Print(Math.Pow(-infinity, 0.5)); // NaN
Print(Math.Pow(-1, infinity)); // NaN
Print(Math.Pow(1, -infinity)); // NaN
```

# 25 输入和输出

顺序输入输出对象称为流（streams）。流有两种类型：字符流和字节流，也称为文本流和二进制流。字符流用于从文本文件输入以及向文本文件、打印机等输出人类可读的内容，使用 16 位 Unicode 字符。字节流用于简单数据（int, double, ...）以及对象和数组的紧凑高效的输入输出。

有不同的类来处理字符流和字节流。字符输入输出类称为 Readers（读取器）和 Writers（写入器）。字节输入输出类称为 Streams。本节使用 System.IO 命名空间描述输入输出。

可以创建流类的子类，通过继承的方法获取专门的流类。此处不再进一步讨论这些。

类层次结构如下表所示，相关的输入和输出类显示在同一行。表格显示了例如 BufferedStream 和 FileStream 是 Stream 的子类，StreamReader 是 TextReader 的子类。抽象类用斜体表示。

| 字符 | 输入流 | 输出流 |
|---|---|---|
| | TextReader | TextWriter |
| | StreamReader | StringWriter |
| | | StreamWriter |
| | BinaryReader | BinaryWriter |
| | Byte | Stream |
| | | FileStream |
| | | BufferedStream |
| | | CryptoStream |
| | | MemoryStream |
| | | NetworkStream |

## 25.1 创建流

输入流或读取器有一个用于读取的数据源，输出流或写入器有一个用于写入的数据汇。流可以直接创建（例如，可以创建一个 StreamReader 并关联磁盘上的命名文件，例如用于从文件读取），也可以从现有流创建以提供额外功能（例如，可以从 Stream 创建 BufferedStream 以实现更高效的输入）。

