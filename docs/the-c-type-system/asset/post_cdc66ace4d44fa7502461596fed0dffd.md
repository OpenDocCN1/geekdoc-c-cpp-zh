
## Abstract Base Types

An abstract type is one that can be used only as a base type for inheritance; it can’t be instantiated directly with new. One implication is that while classes and records can be abstract, structs and record structs can’t. It would make no sense: we can’t inherit from a value type, so it could never be instantiated.

In an abstract type, we can designate methods and properties as abstract, meaning they have no implementation. Their purpose is simply to define the operations that a concrete type must support. An abstract method or property is implicitly virtual, but providing an implementation for one prompts a compiler error. Abstract types don’t have to define any abstract members, but only abstract classes or records can have abstract methods and properties. Any abstract methods or properties remain abstract unless they’re explicitly overridden in a derived class. Providing an implementation for an abstract method in a derived type makes that method concrete.

We can inherit one abstract type from another and choose to either provide implementations for the base type’s abstract methods or leave them as abstract. We can only directly create an instance of a class or record that is fully concrete; that is, any and all abstract methods have been overridden.

If we inherit from an abstract class, we can’t then inherit from any other class because that would be a form of multiple inheritance, which is prohibited.

It can be tempting to think of C# interfaces and their members as being abstract (especially for users familiar with C++, where interfaces are commonly implemented as classes with all pure-virtual methods), but that’s not the case. An interface contains only signatures of methods and properties; they are neither abstract nor virtual.

Inheritance is a central feature of object-oriented code, but it applies exclusively to reference types. Inheritance—as well as the features that support it, such as virtual methods—is not appropriate for value types, in part because of the way value type instances use memory.

## Type Instance Lifetimes

Value types and reference types differ in the way each uses memory and, more specifically, in the lifetime of their instances. Value type instances are short-lived, and their lifetime is bound to the lifetime of the variables that represent them. For value types, the variable is the instance; when we create a new instance of a value type, the target variable effectively contains the instance data—that is, the value of each field of the type.

In many cases, the lifetime of a variable is defined by a block, such as a method body or a foreach loop. Any local variables within the block cease to exist when the block ends. Alternatively, a variable might be contained in another object, in which case the variable’s lifetime is defined by the lifetime of the enclosing object. Whenever we copy a value type variable by assigning it to another variable or passing it as an argument to a method, the copy is a whole new instance of the type in a different variable.

Reference type instances, on the other hand, are generally long-lived and can be referred to by many variables. When we create a new instance of a reference type, we’re given a reference to that instance in memory. Whenever we copy that reference, we’re not also copying the instance. The original reference and the copy both refer to the same instance. References are stored in reference variables.

All reference type instances are allocated on the heap. Their lifetime is managed by automatic garbage collection, which releases their memory when they’re no longer needed by the program. An object is considered unused when the garbage collector determines that no other live references to that instance exist. While reference type instances are not subject to their scope, reference variables are subject to scope, so when one goes out of scope, it’s no longer a live reference to an instance. The lifetime of a reference type instance, then, is determined by the lifetimes of all the references to that instance.

A cost is associated with being allocated on the heap, because the garbage collection process takes time while the program is running. Ensuring that unused heap memory is properly cleaned up is a complex operation and may interrupt a program’s normal execution for a short time, so an overhead is associated with reference types.

Value types don’t require the overhead associated with garbage collection. The memory used by a value type instance can be freed when the lifetime of its variable ends. To understand lifetime a little better, let’s look more closely at what we mean by variable in different contexts.

## Variables

A variable is simply a named area of memory. We use this name—or identifier—to manipulate a memory location during the variable’s lifetime. C# has five main kinds of variables:

### Local variables

These are block-scope variables, where a block might be a method with a statement body, the body of a loop, or any section of code delimited by matching braces, {}. When control leaves a block at the closing brace, any variables that are local to the block go out of scope. When an exception is thrown in a block, the control flow also leaves that scope and any containing scope until the exception is caught or the program exits.

### Instance fields

These are normal data members, known as fields, of structs and non-static classes. Each instance of a type has its own copies of any instance fields. The lifetime of an instance field is defined by the lifetime of the object to which it belongs.

### Static fields

These fields are associated with a type, rather than individual instances of the type. The lifetime of a static field is normally tied to an application, so the instances associated with static fields are usually released when an application exits.

### Array elements

Individual elements in an array are all variables. We can access a particular element by its index and alter the element instance if it is mutable.

### Method parameters

The parameters in a method definition are technically called formal parameters but are commonly known as just parameters. A parameter’s scope is the body of the method, exactly as if the parameter were declared as a local variable within the method’s body. In code that calls a method, we pass actual parameters, better known as arguments, that correspond to the method’s parameters.

Regardless of its kind, a variable always has an associated type. This might be an explicitly declared type, as in the declaration int size, or, for local variables, the type might be implied with the var keyword. If the variable’s type is a reference type, the variable’s value is a reference. A non-null reference is a handle to an instance somewhere on the heap. If the variable’s type is a value type, the variable’s value is an instance of the type.

## Variables vs. Values

It’s not always easy to intuit what counts as a variable and what counts as a value, but the distinction is important:

- Variables can be assigned to, although a readonly field variable can be assigned only within a constructor of the type of which it is a member, or using field initialization (which we’ll discuss in “Field Initializers” on page 58).
- Values are the results of expressions—such as the result of calling new, the return value from a method, or a constant expression such as a literal number or string literal. Values can’t be assigned to, but we use them to initialize variables by using assignment or passing them as arguments to method parameters.
