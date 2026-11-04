
```csharp
rows = r;
cols = c;
a = new int[rows, cols];
Length = rows * cols;
}

// This is the indexer for FailSoftArray2D.
public int this[int index1, int index2] {
    // This is the get accessor.
    get {
        if(ok(index1, index2)) {
            ErrFlag = false;
            return a[index1, index2];
        } else {
            ErrFlag = true;
            return 0;
        }
    }

    // This is the set accessor.
    set {
        if(ok(index1, index2)) {
            a[index1, index2] = value;
            ErrFlag = false;
        } else
            ErrFlag = true;
    }
}

// Return true if the indexes are within bounds.
private bool ok(int index1, int index2) {
    if(index1 >= 0 & index1 < rows &
       index2 >= 0 & index2 < cols)
        return true;

    return false;
}
}

// Demonstrate a 2D indexer.
class TwoDIndexDemo {
    static void Main() {
        FailSoftArray2D fs = new FailSoftArray2D(3, 5);
        int x;

        // Show quiet failures.
        Console.WriteLine("Fail quietly.");
        for(int i=0; i < 6; i++)
            fs[i, i] = i*10;

        for(int i=0; i < 6; i++) {
            x = fs[i, i];
            if(x != -1) Console.Write(x + " ");
        }

        Console.WriteLine();

        // Now, display failures.
        Console.WriteLine("\nFail with error reports.");
        for(int i=0; i < 6; i++) {
            fs[i, i] = i*10;
            if(fs.ErrFlag)
                Console.WriteLine("fs[" + i + "," + i + "] out-of-bounds");
        }

        for(int i=0; i < 6; i++) {
            x = fs[i, i];
            if(!fs.ErrFlag)
                Console.Write(x + " ");
            else
                Console.WriteLine("fs[" + i + "," + i + "] out-of-bounds");
        }
    }
}
```

该程序的输出如下所示：

```text
Fail quietly.
0 10 20 0 0 0

Fail with error reports.
fs[3, 3] out-of-bounds
fs[4, 4] out-of-bounds
fs[5, 5] out-of-bounds
0 10 20 fs[3, 3] out-of-bounds
fs[4, 4] out-of-bounds
fs[5, 5] out-of-bounds
```

## 属性

另一种类型的类成员是属性。

一般来说，属性将字段与其访问方法结合在一起。

正如本书中一些示例所示，您通常希望创建一个对对象用户可用的字段，但您希望对该字段允许的操作保持控制。

例如，您可能希望限制可以分配给该字段的值范围。

虽然可以通过使用私有变量以及访问其值的方法来实现这一目标，但属性提供了一种更好、更简洁的方法。

属性与索引器类似。

属性由名称以及 get 和 set 访问器组成。

访问器用于获取和设置变量的值。

属性的关键优势在于，其名称可以在表达式和赋值中使用，就像普通变量一样，但实际上 get 和 set 访问器会被自动调用。

这与索引器的 get 和 set 访问器自动使用的方式类似。

属性的一般形式如下所示：

```csharp
type name {
    get {
        // get accessor code
    }
}
```

该程序的输出如下所示：

```text
Original value of ob.MyProp: 0
Value of ob.MyProp: 100
Attempting to assign -10 to ob.MyProp
Value of ob.MyProp: 100
```

让我们仔细检查这个程序。

该程序定义了一个私有字段，名为 **prop**，以及一个名为 **MyProp** 的属性来管理对 **prop** 的访问。

如前所述，属性本身并不定义存储位置。

相反，大多数属性只是管理对字段的访问。

此外，由于 **prop** 是私有的，它只能通过 **MyProp** 访问。

属性 **MyProp** 指定为 **public**，以便可以在其类外部的代码中访问它。

这是有意义的，因为它提供了对 **prop** 的访问，而 **prop** 是私有的。

**get** 访问器只是返回 **prop** 的值。

**set** 访问器仅当该值为正时才设置 **prop** 的值。

因此，**MyProp** 属性控制 **prop** 可以具有什么值。

这就是属性重要的本质。

**MyProp** 定义的属性类型称为读写属性，因为它允许读取和写入其底层字段。

然而，也可以创建只读和只写属性。

要创建只读属性，只定义 **get** 访问器。

要定义只写属性，只定义 **set** 访问器。

您可以使用属性进一步改进 fail-soft 数组类。

如您所知，所有数组都有一个关联的 **Length** 属性。

到目前为止，**FailSoftArray** 类只是为此目的使用了一个名为 **Length** 的公共整数字段。

然而，这不是良好的做法，因为它允许将 **Length** 设置为除 fail-soft 数组长度之外的某个值。

（例如，恶意程序员可能会故意破坏其值。）

我们可以通过将 **Length** 转换为只读属性来解决这个问题，如下所示的 **FailSoftArray** 版本所示：

```csharp
// Add Length property to FailSoftArray.

using System;

class FailSoftArray {
    int[] a; // reference to underlying array
    int len; // length of array -- underlies Length property

    public bool ErrFlag; // indicates outcome of last operation

    // Construct array given its size.
    public FailSoftArray(int size) {
        a = new int[size];
        len = size;
    }

    // Read-only Length property.
    public int Length {
        get {
            return len;
        }
    }

    // This is the indexer for FailSoftArray.
    public int this[int index] {
        // This is the get accessor.
        get {
            if(ok(index)) {
                ErrFlag = false;
                return a[index];
            } else {
                ErrFlag = true;
                return 0;
            }
        }

        // This is the set accessor.
        set {
            if(ok(index)) {
                a[index] = value;
                ErrFlag = false;
            }
            else ErrFlag = true;
        }
    }

    // Return true if index is within bounds.
    private bool ok(int index) {
        if(index >= 0 & index < Length) return true;
        return false;
    }
}

// Demonstrate the improved fail-soft array.
class ImprovedFSDemo {
    static void Main() {
        FailSoftArray fs = new FailSoftArray(5);
        int x;

        // Can read Length.
        for(int i=0; i < fs.Length; i++)
            fs[i] = i*10;

        for(int i=0; i < fs.Length; i++) {
            x = fs[i];
            if(x != -1) Console.Write(x + " ");
        }
        Console.WriteLine();
        // fs.Length = 10; // Error, illegal!
    }
}
```

Length 现在是一个属性，使用私有变量 len 作为其存储。

Length 只定义了 get 访问器，这意味着它是只读的。

因此，Length 可以被读取，但不能被更改。

为了证明这一点，请尝试删除程序中该行前的注释符号：

```csharp
// fs.Length = 10; // Error, illegal!
```

当您尝试编译时，您将收到一条错误消息，指出 Length 是只读的。

尽管添加 Length 属性改进了 FailSoftArray，但这并不是属性可以做出的唯一改进。

ErrFlag 成员也是转换为属性的理想候选者，因为对其的访问也应限制为只读。

这是 FailSoftArray 的最终改进。它创建了一个名为 Error 的属性，使用原始的 ErrFlag 变量作为其存储，并且 ErrFlag 被设为 FailSoftArray 私有。

```csharp
// Convert ErrFlag into a property.
using System;

class FailSoftArray {
    int[] a; // reference to underlying array
    int len; // length of array

    bool ErrFlag; // now private

    // Construct array given its size.
    public FailSoftArray(int size) {
        a = new int[size];
        len = size;
    }

    // Read-only Length property.
    public int Length {
        get {
            return len;
        }
    }

    // Read-only Error property.
    public bool Error {
        get {
            return ErrFlag;
        }
    }

    // This is the indexer for FailSoftArray.
    public int this[int index] {
        // This is the get accessor.
        get {
            if(ok(index)) {
                ErrFlag = false;
                return a[index];
            } else {
                ErrFlag = true;
                return 0;
            }
        }
    }
}
```
