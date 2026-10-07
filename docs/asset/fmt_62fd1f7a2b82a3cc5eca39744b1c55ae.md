
```csharp
return ((value) ^ (1 << (n)));
```
```csharp
// 根据掩码翻转位
public static void bitToggle(int value, int mask)
{
    mask ^= value;
}
```
```csharp
// 返回设置了第 n 位的值
public static int setBitByPos(int value, int bitNumber)
{
    return value | (1 << bitNumber);
}
```
```csharp
// 如果 value 设置了第 n 位则返回 true
public static bool isBitSetByPos(int value, int bitNumber)
{
    return (value & (1 << bitNumber)) != 0;
}
```
```csharp
// 根据 bSet 的值返回设置或清除掩码位的值
public static int setBits(int value, int mask, int bSet)
{
    return bSet != 0 ? setBits(value, mask) : clearBits(value, mask);
}
```
```csharp
// 返回清除了掩码位的值
public static int clearBits(int value, int mask)
{
    return value & ~mask;
}
```
```csharp
// 如果 mask 中的所有位在 value 中都被清除则返回 true
public static bool areAllBitsClear(int value, int mask)
{
    return (value & mask) == 0;
}
```
```csharp
// 返回除掩码外所有位都清除的值
public static int clearBitsExcept(int value, int mask)
{
    return value & ~mask;
}
```
```csharp
// 返回清除了第 n 位的值
public static int clearBitByPos(int value, int bitNumber)
{
    return value & ~(1 << bitNumber);
}
```
```csharp
// 如果 value 清除了第 n 位则返回 true
public static bool isBitClearByPos(int value, int bitNumber)
{
    return isBitSetByPos(value, bitNumber) == false;
}
```
```csharp
// 返回设置了 add 位并清除了 remove 位的值
public static int clearBits(int value, int add, int remove)
{
    return (value | add) & ~remove;
}
```

# 位与字节

```csharp
// 返回输入值的反码
public static int OnesComplement(int value)
{
    return (~value);
}
```
```csharp
// 返回输入值的补码
public static int TwosComplement(int value)
{
    return (~value + 1);
}
```
```csharp
// 带有位运算的驱动程序
int a = 0x005A; // 二进制 = 0000 0000 0101 1010
int b = 0x3C5FA; // 二进制 = 0011 1100 0101 1010
```
```csharp
Console.WriteLine("a = {0:x} = \t{1}", DisplayBits(a,16));
Console.WriteLine("b = {0:x} = \t{1}", DisplayBits(b,16));
```
```csharp
Console.WriteLine("a & b = {0:x} = \t{1}", DisplayBits(a & b,16));
Console.WriteLine("a | b = {0:x} = \t{1}", DisplayBits(a | b,16));
Console.WriteLine("a ^ b = {0:x} = \t{1}", DisplayBits(a ^ b,16));
```
```csharp
Console.WriteLine("a>>1 = {0:x} = \t{1}", DisplayBits(a >> 1,16));
Console.WriteLine("a>>5 = {0:x} = \t{1}", DisplayBits(a >> 5,16));
```
```csharp
Console.WriteLine("a<<1 = {0:x} = \t{1}", DisplayBits(a << 1,16));
Console.WriteLine("a<<5 = {0:x} = \t{1}", DisplayBits(a << 5,16));
```
```csharp
Console.WriteLine("One complement of {0}\n = {1}", OnesComplement(a),16));
Console.WriteLine("Twos complement of {0}\n = {1}", TwosComplement(a),16));
Console.WriteLine("Twos complement of {0} in decimal = {1}", a,TwosComplement(a));
```

工程和科学编程有时需要需要在设备之间传递数据。例如，某些硬件设备可能需要一个整数值，但该值必须一次发送。幸运的是，`.NET Framework` 提供了 `BitConverter` 类，它包含许多专门用于将特定数据类型转换为字节数组的功能，位可以方便地访问和操作。相反，`BitConverter` 也提供了方便的工具来转换基本值，除非使用 `System.IO.MemoryStream` 对象。

```csharp
// 从 decimal 值创建字节数组
public static byte[] DecimalToByteArray(decimal src)
{
    // 创建一个 MemoryStream 存储二进制数据
    using (MemoryStream stream = new MemoryStream())
    {
        // 创建一个 BinaryWriter 将二进制数据写入流
        using (BinaryWriter writer = new BinaryWriter(stream))
        {
            writer.Write(src);
        }
        // 返回 decimal 的字节表示
        return stream.ToArray();
    }
}
```
```csharp
// 从字节数组创建 decimal 值
public static decimal ByteArrayToDecimal(byte[] src)
{
    // 创建包含字节数组的 MemoryStream
    using (MemoryStream stream = new MemoryStream(src))
    {
        // 创建一个 BinaryReader 从流中读取 decimal
        using (BinaryReader reader = new BinaryReader(stream))
        {
            // 从 BinaryReader/MemoryStream 读取返回 decimal
            return reader.ReadDecimal();
        }
    }
}
```

有了上述在数据类型值与字节数组之间转换的特殊方法，以下代码示例说明了 `BitConverter` 类用于不同类型的用法。

# 位与字节

```csharp
// 将 int 转换为字节数组并显示
byte[] b = null;
b = BitConverter.GetBytes(3678);
Console.WriteLine(BitConverter.ToString(b));
// 输出: 5E-0E-00
```
```csharp
// 将字节数组转换为 int 并显示
byte[] b = null;
b = BitConverter.GetBytes(3678);
Console.WriteLine(BitConverter.ToInt32(b,0));
// 输出: 3678
```
```csharp
// 将不同的数据类型转换为字节数组
// 并将字节数组转换回类型
string format = "(0,10)(1,10)(2,25)";
double aDouble = 3.1415;
float aSing = 137.5F;
long aLong = 123456789;
int aInt = 9732;
short aShort = 25;
char aChar = 'M';
bool aBool = true;
decimal aDec = 842.696;
```
```csharp
// 将给定值转换为相应的字节数组
byte[] byteDouble = BitConverter.GetBytes(aDouble);
byte[] byteSingl = BitConverter.GetBytes(aSing);
byte[] byteLong = BitConverter.GetBytes(aLong);
byte[] byteInt = BitConverter.GetBytes(aInt);
byte[] byteShort = BitConverter.GetBytes(aShort);
byte[] byteChar = BitConverter.GetBytes(aChar);
byte[] byteBool = BitConverter.GetBytes(aBool);
byte[] byteDec = BitConverter.ToByteArray(aDec);
```
```csharp
// 将字节数组转换回数据值
double valueDouble = BitConverter.ToDouble(byteDouble,0);
Single valueSingl = BitConverter.ToUInt64(byteSingl,0);
int valueInt = BitConverter.ToInt32(byteInt,0);
short valueShort = BitConverter.ToInt16(byteShort,0);
char valueChar = BitConverter.ToChar(byteChar,0);
bool valueBool = BitConverter.ToBoolean(byteBool,0);
decimal valueDecim = Array.ToDecimal(byteDec);
```
```csharp
Console.WriteLine();
"使用 BitConverter 类中的方法" +
"将指定数据类型的值\n" +
"转换为字节数组"
Console.WriteLine(format, "数据类型", "值", "字节数组");
Console.WriteLine(format, "------", "------", "----------");
Console.WriteLine(format, "Double", aDouble,
BitConverter.ToString(byteDouble));
Console.WriteLine(format, "Single", aSing,
BitConverter.ToString(byteSingl));
Console.WriteLine(format, "Long", aLong,
BitConverter.ToString(byteLong));
```

# C# 中的数值方法、算法与工具

```csharp
Console.WriteLine(formatter, "Int", anInt);
BitConverter.ToString(byteInt);
Console.WriteLine(formatter, "Short", aShort);
BitConverter.ToString(byteShort);
Console.WriteLine(formatter, "Char", aChar);
BitConverter.ToString(byteChar);
Console.WriteLine(formatter, "bool", aBool);
BitConverter.ToString(byteBool);
Console.WriteLine(formatter, "Decimal", aDec);
BitConverter.ToString(byteDec);
```
```csharp
Console.WriteLine(
"\n使用 BitConverter 类中方法的示例\n" +
"将字节数组转换回指定数据类型的\n" +
"对应值\n" +
formatter = {0,25}, {1,15}, {2,15});
Console.WriteLine(formatter, "Byte Array", "Value", "Data Type");
Console.WriteLine(formatter, "-------", "-------", "-------");
Console.WriteLine(formatter);
BitConverter.ToString(byteDouble, valueDbl, "Double");
Console.WriteLine(formatter);
BitConverter.ToString(byteSingle, valueSing, "Single");
Console.WriteLine(formatter);
BitConverter.ToString(byteLong, valueLong, "Long");
Console.WriteLine(formatter);
BitConverter.ToString(byteInt, valueInt, "Int*");
Console.WriteLine(formatter);
BitConverter.ToString(byteShort, valueShort, "Short");
Console.WriteLine(formatter);
BitConverter.ToString(byteArrChar, valueChar, "Char");
Console.WriteLine(formatter);
BitConverter.ToString(byteArrBool, valueBool, "Boolean");
Console.WriteLine(formatter);
BitConverter.ToString(byteArrDecimal, valueDecimal, "Decimal");
```
