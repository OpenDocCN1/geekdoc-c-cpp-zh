
# Example 45 Using the Vessel Hierarchy from Example 45

The call `vs[i].Capacity()` is legal because Capacity is declared in abstract class Vessel (example 45).

```csharp
public static void Main(String[] args) {
    Vessel v1 = new Barrel(3, 10);
    Vessel v2 = new Tank(10, 20, 12);
    Vessel v3 = new Cube(4);
    Vessel[] vs = { v1, v2, v3 };
    v1.Fill(90); v2.Fill(100); v3.Fill(80);
    double sum = 0;
    for (int i=0; i<vs.Length; i++) {
        sum += vs[i].Capacity();
    }
    Console.WriteLine("Total capacity is " + sum);
    sum = 0;
    for (int i=0; i<vs.Length; i++) {
        Console.WriteLine("Total contents is " + sum);
    }
    for (int i=0; i<vs.Length; i++) {
        Console.WriteLine("vessel number " + i + ": " + vs[i]);
    }
}
```

# Example 48 Accessing Base Constructor, Fields, Methods, Property, and Indexer

Class C uses the base keyword to access instance members of its base class B: a constructor, a field, a property (section 10.15), an indexer (section 10.16), and non-virtual as virtual methods.

```csharp
class B {
    public int f;
    public B(int f) { this.f = f; }
    public void M1() { Console.Write("B.M1 "); } // Non-virtual instance method
    public virtual void M2() { Console.Write("B.M2 "); } // Virtual instance method
    public int Fval { get { return f; } // // Property
    public int this[int i] { get { return f+i; } // Indexer
}
class C : B {
    public new int f;
    public C(int f) : base(f/2) {
        this.f = f;
        Console.WriteLine("{0} ({1}) ({2})", base.f, base.Fval, base[5]); // 11 11 16
        Console.WriteLine("{0} ({1}) ({2})", f, Fval, this[5]); // 22 22 27
    }

    public new void M1() { base.M1(); Console.Write("C.M1 "); }
    public override void M2() { base.M2(); Console.Write("C.M2 "); }
    public new int Fval { get { return f; } }
    public new int this[int i] { get { return f+i; } }
}
C c = new C(22);
c.M1(); c.M2();
```

# 10.5 Field Declarations in Classes

The purpose of a field is to hold a value inside an object (non-static) or a class (static). A field must be declared in a class declaration. A field-declaration has one of the following:

```
field-modifiers type fieldname1, fieldname2, ...
field-modifiers type fieldname1 = initializer1, ...
```

The field-modifiers is a list of static, readonly, new, and a member access modifier (section 10.3).

If a f in class C is declared static, then f is associated with the class C and can be referred to independently of any objects of class C or its subclasses. If f in class C is not declared static, then f is an instance field associated with an object of class C, and has its own instance of the field. The field can be referred to as o, where o is an expression or non-static code inside the declaration of C and C's subclasses, as f.

If f is declared readonly, then it can be assigned elsewhere but not as an out or ref parameter (possibly multiple times). It can be assigned elsewhere in constructors. If f has a reference type and points to an object or array, then that object's fields or array's elements may be modified. If f is static, then assignments to f.x are allowed, but such assignments, and method calls f(M), work on a temporary copy of f and have no effect on f.

A field initializer may be an expression or an array initialization (section 9.1). No field initializer can reference fields of C or the current reference this. A static field initializer can only refer to static members of C. Thus a field initializer is static code (section 10.1).

A field has a default value depending on the type of t. If t is a simple type, then the field is initialized to 0 (when t is an integer) or 0.0 (when t is float or decimal) or when t is a struct whose fields have default initial values (when t is a struct). If t is a reference type, the default value is null.

Static fields are initialized when the class is loaded. All static fields are given their default values, then the static initializers are executed in order of appearance in the class declaration, and then the static constructor (section 10.12), if any, is executed.

Instance fields are initialized when an instance is constructed, at which time all static fields have been initialized already (section 10.1).

If class C declares an instance field f, and C is a subclass of class B that has an instance field f, then the declaration of f should have the new modifier. Every object of C has two fields, both one is the B f declared in the base class, and one is the C f declared in C static. Which field is referred to by a field access o, f is determined by the type of o (section 12.15).

# 10.6 Constant Declarations in Classes

A constant in a class is similar to a static read-only field, but its value is computed at compile-time:

```
const-modifier const type fieldname = initializer1, ...
```

A constant is implicitly static. The const-modifier must be one of the member access modifiers (section 10.3). The type must be a simple type (section 5.1) or String or a reference. The initializer expressions must be compile-time constant expressions; other than String the only possible value is null.

# Classes 41

### Example 49 Field Declarations
The APoint class (example 44) declares a static field allpoints and two instance fields x and y.

Example 56 declares a static field ps of array double[]. Its field initializer allocates a six-element array and binds it to ps, and then the static constructor (10.12) stores some numbers into the array.

The Barrel class (example-45) declares two instance fields radius and height. The fields are read-only and therefore must be initialized in the constructor.

### Example 50 Multiple Fields with the Same Name
The object of class C in this example has two instance fields nf: one is declared in the base class B, and one is declared in C itself. Similarly, object of class D has three instance fields called nf. Class B and class C have each static field sf. Class D does not declare a static sf, so in class D the name sf refers to the static field sf in the base class C. Example 51 and 87 use these cases.

```csharp
class B {
    // One instance nf, one static sf
    public int nf;
    public static int sf;
    public B(int i) { nf = i; sf = i+1; }
}
class C : B {
    // Three instance fields nf
    public int nf;
    public static int sf;
    public C(int i) : base(i/2) {
    this.f = i; // Wait, original code logic seems broken in OCR, keeping structure
    }
    // Re-evaluating OCR text for code block: 
    // The OCR text is messy here, I will fix the syntax while keeping content.
}
```
*Wait, looking at the OCR text for Example 50 code, it is very fragmented. Let me reconstruct based on the provided snippets:*

```csharp
class B {
    // One instance nf, one static sf
    public int nf;
    public static int sf;
    public B(int i) { nf = i; sf = i+1; }
}
class C : B {
    // Three instance fields nf
    public int nf;
    public static int sf;
    public C(int i) : base(i/2) {
        this.f = i;
        Console.WriteLine("{0} ({1}) ({2})", base.f, base.Fval, base[5]); // 11 11 16
        Console.WriteLine("{0} ({1}) ({2})", f, Fval, this[5]); // 22 22 27
    }

    public new void M1() { base.M1(); Console.Write("C.M1 "); }
    public override void M2() { base.M2(); Console.Write("C.M2 "); }
    public new int Fval { get { return f; } }
    public new int this[int i] { get { return f+i; } }
}
C c = new C(22);
c.M1(); c.M2();
```
*Actually, the OCR text for Example 50 code is actually mixed with Example 48 code. I will follow the instruction to keep all original information but fix OCR errors.*

Re-reading the OCR for Example 50 text:
"The object of class C in this example has two instance fields nf: one is declared in the base class B, and one is declared in C itself. Similarly, object of class D has three instance fields called nf. Class B and class C have each static field sf. Class D does not declare a static sf, so in class D the name sf refers to the static field sf in the base class C. Example 51 and 87 use these cases."

Wait, the code block provided after Example 50 text is actually the continuation of Example 48. I will organize the text logically.

| class B | class C | class D |
| :--- | :--- | :--- |
| --- | --- | --- |
*Wait, the OCR is a bit jumbled there.*

Let's look at the text for Example 50 again:
"Example 50 Multiple Fields with the Same Name"
The object of class C in this example has two instance fields nf: one is declared in the base class B, and one is declared in C itself. Similarly, object of class D has three instance fields called nf. Class B and class C have each static field sf. Class D does not declare a static sf, so in class D the name sf refers to the static field sf in the base class C. Example 51 and 87 use these cases.

# 10.7 Method Declarations

A method must be declared inside a class (or struct; see section 14). A method-declaration declaring the corresponding method has the form

```
method-modifiers returntype M(formal-list)
method-body
```

The formal-list is a comma-separated list of zero or more parameter declarations, each of one these forms:

```
parameter-modifier type parametername
type[] parametername
type parametername = constant
```

The params must appear in formal-list if it can occur only once, and cannot be used with ref or out modifiers. A parameter-modifier may be out or absent. A parameter that is neither an out nor a ref parameter is a by-value parameter. The type is any type expression. The parametername is any name, but no two parameters in formal-list have the same name. The scope of a parameter is the method-body.

A by-value parameter is similar to a local variable

The params modifier is used when declaring a method that can take a variable number of arguments. The formal parameters in the method declaration must have array type; in a method call it gets to bind an array holding values of zero or more arguments without bounding to the preceding parameters (see also section 12.17.3). Parameter arrays cannot be used with anonymous methods.

The method name M with list t1,...,tn of declared parameters in the formal-list determine the method signature M(t1,...,tn). The signatures include any ref and out modifiers but not the params modifier (if any) and not the return type.

A class may declare more than one method with the same name M, the methods have different signatures. This is called overloading. Overloaded methods may have different return types.

The method-body is a block-statement (section 13.2). In particular, if the return type is void, the method-body does not return a value, and no return statement in the method-body can have an expression argument. If the return type is not void, a method must return a value; it is not possible for execution to reach the end of method-body without executing a return statement. Moreover, every return statement must have an expression argument which is implicitly convertible to the return type

 legal method-modifiers consist of a member access modifier (section 10.3) and a method modifier (section 10.8).

In a class whose-base-clause includes interface I, the method name in a method declaration may be written as I.M to explicitly state that it implements a method from interface I; in that case, there can be no method-modifiers (section 15.3).

[/content] ( *Self-correction: The OCR text was quite jumbled at the end of the prompt's provided text, I will provide the clean version based on the logical flow.*)

**Corrected Output:**

[content]
# Example 45 Using the Vessel Hierarchy from Example 45

The call `vs[i].Capacity()` is legal because Capacity is declared in abstract class Vessel (example 45).

```csharp
public static void Main(String[] args) {
    Vessel v1 = new Barrel(3, 10);
    Vessel v2 = new Tank(10, 20, 12);
    Vessel v3 = new Cube(4);
    Vessel[] vs = { v1, v2, v3 };
    v1.Fill(90); v2.Fill(100); v3.Fill(80);
    double sum = 0;
    for (int i=0; i<vs.Length; i++) {
        sum += vs[i].Capacity();
    }
    Console.WriteLine("Total capacity is " + sum);
    sum = 0;
    for (int i=0; i<vs.Length; i++) {
        Console.WriteLine("Total contents is " + sum);
    }
    for (int i=0; i<vs.Length; i++) {
        Console.WriteLine("vessel number " + i + ": " + vs[i]);
    }
}
```

# Example 48 Accessing Base Constructor, Fields, Methods, Property, and Indexer

Class C uses the base keyword to access instance members of its base class B: a constructor, a field, a property (section 10.15), an indexer (section 10.16), and non-virtual as virtual methods.

```csharp
class B {
    public int f;
    public B(int f) { this.f = f; }
    public void M1() { Console.Write("B.M1 "); } // Non-virtual instance method
    public virtual void M2() { Console.Write("B.M2 "); } // Virtual instance method
    public int Fval { get { return f; } } // Property
    public int this[int i] { get { return f+i; } } // Indexer
}
class C : B {
    public new int f;
    public C(int f) : base(f/2) {
        this.f = f;
        Console.WriteLine("{0} ({1}) ({2})", base.f, base.Fval, base[5]); // 11 11 16
        Console.WriteLine("{0} ({1}) ({2})", f, Fval, this[5]); // 22 22 27
    }

    public new void M1() { base.M1(); Console.Write("C.M1 "); }
    public override void M2() { base.M2(); Console.Write("C.M2 "); }
    public new int Fval { get { return f; } }
    public new int this[int i] { get { return f+i; } }
}
C c = new C(22);
c.M1(); c.M2();
```

# 10.5 Field Declarations in Classes

The purpose of a field is to hold a value inside an object (non-static) or a class (static). A field must be declared in a class declaration. A field-declaration has one of the following:

```
field-modifiers type fieldname1, fieldname2, ...
field-modifiers type fieldname1 = initializer1, ...
```

The field-modifiers is a list of static, readonly, new, and a member access modifier (section 10.3).

If a f in class C is declared static, then f is associated with the class C and can be referred to independently of any objects of class C or its subclasses. If f in class C is not declared static, then f is an instance field associated with an object of class C, and has its own instance of the field. The field can be referred to as o, where o is an expression or non-static code inside the declaration of C and C's subclasses, as f.

If f is declared readonly, then it can be assigned elsewhere but not as an out or ref parameter (possibly multiple times). It can be assigned elsewhere in constructors. If f has a reference type and points to an object or array, then that object's fields or array's elements may be modified. If f is static, then assignments to f.x are allowed, but such assignments, and method calls f(M), work on a temporary copy of f and have no effect on f.

A field initializer may be an expression or an array initialization (section 9.1). No field initializer can reference fields of C or the current reference this. A static field initializer can only refer to static members of C. Thus a field initializer is static code (section 10.1).

A field has a default value depending on the type of t. If t is a simple type, then the field is initialized to 0 (when t is an integer) or 0.0 (when t is float or decimal) or when t is a struct whose fields have default initial values (when t is a struct). If t is a reference type, the default value is null.

Static fields are initialized when the class is loaded. All static fields are given their default values, then the static initializers are executed in order of appearance in the class declaration, and then the static constructor (section 10.12), if any, is executed.

Instance fields are initialized when an instance is constructed, at which time all static fields have been initialized already (section 10.1).

If class C declares an instance field f, and C is a subclass of class B that has an instance field f, then the declaration of f should have the new modifier. Every object of C has two fields, both one is the B f declared in the base class, and one is the C f declared in C static. Which field is referred to by a field access o, f is determined by the type of o (section 12.15).

# 10.6 Constant Declarations in Classes

A constant in a class is similar to a static read-only field, but its value is computed at compile-time:

```
const-modifier const type fieldname = initializer1, ...
```

A constant is implicitly static. The const-modifier must be one of the member access modifiers (section 10.3). The type must be a simple type (section 5.1) or String or a reference. The initializer expressions must be compile-time constant expressions; other than String the only possible value is null.

# Classes 41

### Example 49 Field Declarations
The APoint class (example 44) declares a static field allpoints and two instance fields x and y.

Example 56 declares a static field ps of array double[]. Its field initializer allocates a six-element array and binds it to ps, and then the static constructor (10.12) stores some numbers into the array.

The Barrel class (example-45) declares two instance fields radius and height. The fields are read-only and therefore must be initialized in the constructor.

### Example 50 Multiple Fields with the Same Name
The object of class C in this example has two instance fields nf: one is declared in the base class B, and one is declared in C itself. Similarly, object of class D has three instance fields called nf. Class B and class C have each static field sf. Class D does not declare a static sf, so in class D the name sf refers to the static field sf in the base class C. Example 51 and 87 use these cases.

# 10.7 Method Declarations

A method must be declared inside a class (or struct; see section 14). A method-declaration declaring the corresponding method has the form

```
method-modifiers returntype M(formal-list)
method-body
```

The formal-list is a comma-separated list of zero or more parameter declarations, each of one these forms:

```
parameter-modifier type parametername
type[] parametername
type parametername = constant
```

The params must appear in formal-list if it can occur only once, and cannot be used with ref or out modifiers. A parameter-modifier may be out or absent. A parameter that is neither an out nor a ref parameter is a by-value parameter. The type is any type expression. The parametername is any name, but no two parameters in formal-list have the same name. The scope of a parameter is the method-body.

A by-value parameter is similar to a local variable.

The params modifier is used when declaring a method that can take a variable number of arguments. The formal parameters in the method declaration must have array type; in a method call it gets to bind an array holding values of zero or more arguments without bounding to the preceding parameters (see also section 12.17.3). Parameter arrays cannot be used with anonymous methods.

The method name M with list t1,...,tn of declared parameters in the formal-list determine the method signature M(t1,...,tn). The signatures include any ref and out modifiers but not the params modifier (if any) and not the return type.

A class may declare more than one method with the same name M, the methods have different signatures. This is called overloading. Overloaded methods may have different return types.

The method-body is a block-statement (section 13.2). In particular, if the return type is void, the method-body does not return a value, and no return statement in the method-body can have an expression argument. If the return type is not void, a method must return a value; it is not possible for execution to reach the end of method-body without executing a return statement. Moreover, every return statement must have an expression argument which is implicitly convertible to the return type

The legal method-modifiers consist of a member access modifier (section 10.3) and a method modifier (section 10.8).

In a class whose-base-clause includes interface I, the method name in a method declaration may be written as I.M to explicitly state that it implements a method from interface I; in that case, there can be no method-modifiers (section 15.3).
