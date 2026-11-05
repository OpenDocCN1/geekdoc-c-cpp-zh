
```csharp
public IEnumerator<T> GetEnumerator() {
    if (left != null) foreach (T x in left) yield x;
    yield value;
    if (right != null) foreach (T x in right) yield x;
}
}
class Program
{
    static Tree<T> MakeTree<T>(T[] items, int left, int right) {
        if (left > right) return null;
        int i = (left + right) / 2;
        return new Tree<T>(items[i]);
        MakeTree(items, left, i - 1);
        MakeTree(items, i + 1, right);
    }

    static Tree<T> MakeTree<T>(params T[] items) {
        return MakeTree(items, 0, items.Length - 1);
    }

    // The output of the program is:
    // 1 2 3 4 5 6 7 8 9
    // Mon Tue Wed Thu Fri Sat Sun
    static void Main() {
        Tree<int> ints = MakeTree(1, 2, 3, 4, 5, 6, 7, 8, 9);
        foreach (int i in ints) Console.Write("{0} ", i);
        Console.WriteLine();
        Tree<string> strings = MakeTree(
            "Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun");
        foreach (string s in strings) Console.Write("{0} ", s);
        Console.WriteLine();
    }
}
```

The GetEnumerator method can be translated into an instantiation of a compiler-generated enumerator class that encapsulates the code in the iterator block, as shown in the following.

```csharp
class Tree<T>: IEnumerable<T>
{
    ...

    public IEnumerator<T> GetEnumerator() {
        return new __Enumerator1(this);
    }
    class __Enumerator1 : IEnumerator<T>, IEnumerator
    {
        Tree<T> __this;
        IEnumerator<T> __left, __right;
        int __state;
        T __current;

        public __Enumerator1(Tree<T> __this) {
            this.__this = __this;
        }

        public T Current {
            get { return __current; }
        }

        object IEnumerator.Current {
            get { return __current; }
        }
    }
}
```

```csharp
public bool MoveNext() {
    try {
        switch (__state) {
            case 0:
                __state = -1;
                if (__this.left == null) goto __yield_value;
                __left = __this.left.GetEnumerator();
                goto case 1;
            case 1:
                __state = -2;
                if (!__left.MoveNext()) goto __left_dispose;
                __current = __left.Current;
                __state = 1;
                return true;
            __left_dispose:
                __state = -1;
                __left.Dispose();
            __yield_value:
                __current = __this.value;
                __state = 2;
                return true;
            case 2:
                __state = -1;
                if (__this.right == null) goto __end;
                __right = __this.right.GetEnumerator();
                goto case 3;
            case 3:
                __state = -3;
                if (!__right.MoveNext()) goto __right_dispose;
                __current = __right.Current;
                __state = 3;
                return true;
            __right_dispose:
                __state = -1;
                __right.Dispose();
            __end:
                __state = 4;
                break;
        }
    }
    finally {
        if (__state < 0) Dispose();
    }
    return false;
}
public void Dispose() {
    try {
        switch (__state) {
            case 1:
            case 2:
                __left.Dispose();
                break;
            case 3:
            case -3:
                __right.Dispose();
                break;
        }
    }
}
```

```csharp
}
    finally {
        __state = 4;
    }
}
    void IEnumerator.Reset() {
        throw new NotSupportedException();
    }
}
```

The compiler generated temporaries used in the foreach statements are lifted into the __left and __right fields of the enumerator object. The __state field of the enumerator object is carefully updated so that the correct Dispose() method will be called correctly if an exception is thrown. Note that it is not possible to write the translated code with simple foreach statements.

## 11. Structs

Structs are similar to classes in that they represent data structures that can contain data members and function members. However, unlike classes, structs are value types and do not require heap allocation. A variable of a struct type directly contains the data of the struct, whereas a variable of a class type contains a reference to the data, the latter known as an object.

Structs are particularly useful for small data structures that have value semantics. Complex numbers, points in a coordinate system, or key-value pairs in a dictionary are all good examples of structs. Key to these data structures is that they have few data members, that they do not require use of inheritance or referential identity, and that they can be conveniently implemented using value semantics where assignment copies the value instead of the reference.

As described in §4.1.4, the simple types provided by C#, such as int, double, and bool, are in fact all struct types. Just as these predefined types are structs, it is also possible to use structs and operator overloading to implement new “primitive” types in the C# language. Two examples of such types are given at the end of this chapter (§11.4).

### 11.1 Struct declarations

A struct-declaration is a type-declaration (§9.6) that declares a new struct:

```
struct-declaration:
    attributesopt struct-modifiersopt partialopt struct identifier type-parameter-listopt
    struct-interfacesopt type-parameter-constraints-clausesopt struct-body ;opt
```

A struct-declaration consists of an optional set of attributes (§17), followed by an optional set of struct-modifiers (§11.1.1), followed by an optional partial modifier, followed by the keyword struct and an identifier that names the struct, followed by an optional type-parameter-list specification (§10.1.3), followed by an optional struct-interfaces specification (§11.1.2 ), followed by an optional type-parameters-constraints-clauses specification (§10.1.5), followed by a struct-body (§11.1.4), optionally followed by a semicolon.

#### 11.1.1 Struct modifiers

A struct-declaration may optionally include a sequence of struct modifiers:

```
struct-modifiers:
    struct-modifier
    struct-modifier struct-modifier

struct-modifier:
    new
    public
    protected
    internal
    private
```

It is a compile-time error for the same modifier to appear multiple times in a struct declaration.

The modifiers of a struct declaration have the same meaning as those of a class declaration (§10.1).

#### 11.1.2 Partial modifier

The partial modifier indicates that this struct-declaration is a partial type declaration. Multiple partial struct declarations with the same name within an enclosing namespace or type declaration combine to form one struct declaration, following the rules specified in §10.2.

#### 11.1.3 Struct interfaces

A struct declaration may include a struct-interfaces specification, in which case the struct is said to directly implement the given interface types.

```
struct-interfaces:
    : interface-type-list
```

Interface implementations are discussed further in §13.4.

#### 11.1.4 Struct body

The struct-body of a struct defines the members of the struct.

```
struct-body:
    { struct-member-declarationsopt }
```

### 11.2 Struct members

The members of a struct consist of the members introduced by its struct-member-declarations and the members inherited from the type System.ValueType.

```
struct-member-declarations:
    struct-member-declaration
    struct-member-declarations struct-member-declaration
```

```
struct-member-declaration:
    constant-declaration
    field-declaration
    method-declaration
    property-declaration
    event-declaration
    indexer-declaration
    operator-declaration
    constructor-declaration
    static-constructor-declaration
    type-declaration
```

Except for the differences noted in §11.3, the descriptions of class members provided in §10.3 through §10.14 apply to struct members as well.

### 11.3 Class and struct differences

Structs differ from classes in several important ways:

- Structs are value types (§11.3.1).
- All struct types implicitly inherit from the class System.ValueType (§11.3.2).
- Assignment to a variable of a struct type creates a copy of the value being assigned (§11.3.3).
- The default value of a struct is the value produced by setting all value type fields to their default value and all reference type fields to null (§11.3.4).
- Boxing and unboxing operations are used to convert between a struct type and object (§11.3.5).
