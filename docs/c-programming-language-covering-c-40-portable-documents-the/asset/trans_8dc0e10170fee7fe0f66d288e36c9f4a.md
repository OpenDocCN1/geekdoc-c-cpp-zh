
## 11.3.9 析构函数

结构不允许声明析构函数。

## 11.3.10 静态构造函数

结构的静态构造函数遵循与类的大多数相同规则。结构类型的静态构造函数的执行由应用程序域中发生的以下第一个事件触发：

- 引用结构类型的静态成员。
- 调用结构类型的显式声明的构造函数。

创建结构类型的默认值（§11.3.4）不会触发静态构造函数。（这方面的一个示例是数组中元素的初始值。）

## 11.4 结构示例

下面展示了两个重要示例，说明如何使用结构类型创建可与该语言内置类型类似使用、但具有修改后语义的类型。

> > **比尔·瓦格纳** 由于语言和框架中已添加可空类型，这些示例现在不再那么有说服力。即便如此，我发现，当我创建非常大的数据值集合时，我仍然会创建用于保存类型实例的结构类型。

### 11.4.1 数据库整数类型

下面的 DBInt 结构实现了一个整数类型，它可以表示 int 类型的完整值集，外加一个表示未知值的附加状态。具有这些特征的类型通常用于数据库中。

```csharp
using System;
public struct DBInt
{
    // The Null member represents an unknown DBInt value.
    public static readonly DBInt Null = new DBInt();
    // When the defined field is true, this DBInt represents a
    // known value that is stored in the value field. When
    // the defined field is false, this DBInt represents an
    // unknown value, and the value field is 0.
int value;
bool defined;
// Private instance constructor.
// Creates a DBInt with a known value.
DBInt(int value) {
    this.value = value;
    this.defined = true;
}

// The IsNull property is true if this
// DBInt represents an unknown value.
public bool IsNull { get { return !defined; } }
// The Value property is the known value of this DBInt,
// or 0 if this DBInt represents an unknown value.
public int Value { get { return value; } }
// Implicit conversion from int to DBInt.
public static implicit operator DBInt(int x) {
    return new DBInt(x);
}
// Explicit conversion from DBInt to int. Throws an
// exception if the given DBInt represents an unknown value.
public static explicit operator int(DBInt x) {
    if (!x.defined) throw new InvalidOperationException();
    return x.value;
}
public static DBInt operator +(DBInt x) {
    return x;
}
public static DBInt operator -(DBInt x) {
    return x.defined ? -x.value : Null;
}
public static DBInt operator +(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value + y.value: Null;
}
public static DBInt operator -(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value - y.value: Null;
}
public static DBInt operator *(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value * y.value: Null;
}
public static DBInt operator /(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value / y.value: Null;
}
public static DBInt operator %(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value % y.value: Null;
}
public static DBBool operator ==(DBInt x, DBInt y) {
    return x.defined &&
        y.defined? x.value == y.value: DBBool.Null;
}
public static DBBool operator !=(DBInt x, DBInt y) {
    return x.defined &&
        y.defined? x.value != y.value: DBBool.Null;
}
public static DBBool operator >(DBInt x, DBInt y) {
    return x.defined &&
        y.defined? x.value > y.value: DBBool.Null;
}
public static DBBool operator <(DBInt x, DBInt y) {
    return x.defined &&
        y.defined? x.value < y.value: DBBool.Null;
}
public static DBBool operator >=(DBInt x, DBInt y) {
    return x.defined &&
        y.defined? x.value >= y.value: DBBool.Null;
}
public static DBBool operator <=(DBInt x, DBInt y) {
    return x.defined &&
        y.defined? x.value <= y.value: DBBool.Null;
}
public override bool Equals(object obj) {
    if (!(obj is DBInt)) return false;
    DBInt x = (DBInt)obj;
    return value == x.value && defined == x.defined;
}
public override int GetHashCode() {
    return value;
}
public override string ToString() {
    return defined? value.ToString():"DBInt.Null";
}
}
```

> **克里斯蒂安·纳格尔** 在 System.Data.SqlTypes 命名空间中，.NET 包含诸如 SqlBoolean 和 SqlInt32 之类的映射结构，它们与这里的 DBInt 和 DBBool 示例有些相似。这些类型自 .NET 1.0 起就可用，创建它们是为了允许空值，就像原生数据库类型可以做到的那样。鉴于可空类型自 .NET 2.0 起就可用，可以避免创建自定义类型，而改用 int? 和 bool?。

### 11.4.2 数据库布尔类型

下面的 DBBool 结构实现了一个三值逻辑类型。该类型的可能值为 DBBool.True、DBBool.False 和 DBBool.Null，其中 Null 成员表示未知值。此类三值逻辑类型通常用于数据库中。

```csharp
using System;
public struct DBBool
{
    // The three possible DBBool values.
    public static readonly DBBool Null = new DBBool(0);
    public static readonly DBBool False = new DBBool(-1);
    public static readonly DBBool True = new DBBool(1);
    // Private field that stores -1, 0, 1 for False, Null, True.
    sbyte value;
    // Private instance constructor.
    // The value parameter must be -1, 0, or 1.
    DBBool(int value) {
        this.value = (sbyte)value;
    }
    // Properties to examine the value of a DBBool. Return true
    // if this DBBool has the given value, false otherwise.
    public bool IsNull { get { return value == 0; } }
    public bool IsFalse { get { return value < 0; } }
    public bool IsTrue { get { return value > 0; } }
    // Implicit conversion from bool to DBBool. Maps true to
    // DBBool.True and false to DBBool.False.
    public static implicit operator DBBool(bool x) {
        return x ? True : False;
    }
    // Explicit conversion from DBBool to bool.
    // Throws an exception if the given DBBool
    // is Null; otherwise, returns true or false.
    public static explicit operator bool(DBBool x) {
        if (x.value == 0) throw new InvalidOperationException();
        return x.value > 0;
    }
    // Equality operator. Returns Null if either operand is Null;
    // otherwise, returns True or False.
    public static DBBool operator ==(DBBool x, DBBool y) {
        if (x.value == 0 || y.value == 0) return Null;
        return x.value == y.value? True: False;
    }
    // Inequality operator. Returns Null if either operand is Null;
    // otherwise, returns True or False.
    public static DBBool operator !=(DBBool x, DBBool y) {
        if (x.value == 0 || y.value == 0) return Null;
        return x.value != y.value? True: False;
    }

    // Logical negation operator. Returns True if the operand is
    // False, Null if the operand is Null,
    // or False if the operand is True.
    public static DBBool operator !(DBBool x) {
        return new DBBool(-x.value);
    }

    // Logical AND operator. Returns False if either operand is False,
    // otherwise, Null if either operand is Null; otherwise, True.
    public static DBBool operator &(DBBool x, DBBool y) {
        return new DBBool(x.value < y.value? x.value: y.value);
    }

    // Logical OR operator. Returns True if either operand is True;
    // otherwise, Null if either operand is Null; otherwise, False.
    public static DBBool operator |(DBBool x, DBBool y) {
        return new DBBool(x.value > y.value? x.value: y.value);
    }

    // Definitely true operator. Returns true if the
    // operand is True, false otherwise.
    public static bool operator true(DBBool x) {
        return x.value > 0;
    }
    // Definitely false operator. Returns true if the
    // operand is False, false otherwise.
    public static bool operator false(DBBool x) {
        return x.value < 0;
    }

    public override bool Equals(object obj) {
        if (!(obj is DBBool)) return false;
        return value == ((DBBool)obj).value;
    }

    public override int GetHashCode() {
        return value;
    }

    public override string ToString() {
        if (value > 0) return "DBBool.True";
        if (value < 0) return "DBBool.False";
        return "DBBool.Null";
    }
}
```

