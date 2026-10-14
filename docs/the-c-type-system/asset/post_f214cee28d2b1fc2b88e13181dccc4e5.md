
You know from previous chapters that copying references is always a cheap operation, because it doesn’t also copy the instance. When we copy a value type instance, however, the value of each field is also copied, costing time and memory space, especially if the instance consists of several fields. Knowing when copying might occur, then, may help us identify opportunities to avoid some copies, thereby improving our program’s memory usage and speed.

The relative cost difference between copying a reference and copying an instance is part of the rationale behind the common advice to make value types small. However, the cost of copying is only one part of the story. Copying value type instances around is usually cheap, although some pathological cases may be cause for concern, but working with a copy might also have semantic implications. In particular, if we haven’t noticed that we’ve made a copy, we might be surprised that changes we’ve made to a value aren’t visible in the way we expect. Correspondingly, unexpected changes to an instance that have occurred using a copied reference can be the cause of subtle problems.

## Copying by Simple Assignment

The differences in copy behavior of value types and reference types can have subtle consequences that can be hidden in apparently simple expressions that make a copy. The simplest example of copying occurs as the result of assignment:

```
var copy = existing;
```

Assigning the value of one variable to another like this is called simple assignment, and the left side—the target of the assignment—must be either a variable, or a property or indexer with an accessible set accessor. The right side is an expression, which describes anything that can be evaluated to produce a value. The expression might be a simple value like a literal or an enum member, another variable, or a more complex expression, such as a call to a method.

Both variables and values are associated with a type. Since in the preceding example we use type deduction for copy with the var declaration, the compiler deduces the type of the copy variable from the type of the value of existing. The type of the target variable doesn’t necessarily need to be identical to the type of the value being assigned. If we specify a different type for the target variable, the type of the value on the right must be implicitly convertible to the type of the variable on the left.

We can try to explicitly coerce the value to the target type by using an explicit cast, which you saw in Chapter 2. For example, a double can be explicitly cast to an int, although the conversion may lose information because the value is truncated. If the compiler detects that an explicit conversion can never succeed, such as from a string to an int, the code won’t compile. Otherwise, the conversion happens at run time and may fail with an InvalidCastException if the conversion fails.

## Value Copy Behavior

We know a copy of a non-null reference refers to the same instance in memory as the original reference. That means any change we make to an instance of a reference type is visible via all the references to that instance. By comparison, when we copy an instance of a value type, the copy is a new, independent instance of the type, with copies of the original value’s fields.

However, it’s not always the case that changes to one instance of a value type can’t be observed by other instances. If any of the fields copied from the original value type instance are references, the copied instances will have copies of those references. Therefore, a copy of a value type instance can still alias an object on the heap via its fields. To illustrate, consider the ill-advised example in Listing 4-1, where the Item property of the Purchase struct is a reference to a mutable Product class.

```
public sealed class Product
{
    public int      Id { get; set; }
    public decimal  Price { get; set; }
}

public readonly struct Purchase
{
    public Product  Item { get; init; }
    public DateTime Ordered { get; init; }
    public int      Quantity { get; init; }
}
```

Listing 4-1: Mutable reference fields

Here, Product is a simple data-carrier class, similar to types often used to read data from a database or message queue. A common characteristic of simple data carriers like Product is to have mutable properties to read and write their values. The Purchase type, meanwhile, is a struct and a well-behaved value type; it’s marked readonly, and all of its properties are init-only, meaning they can be given a value only when a new Purchase instance is initialized.

Even though Purchase is a readonly struct, it is not immutable because its Item property is a mutable type. Moreover, that property is a reference because Product is a reference type. Two Purchase instances, therefore, can refer to the same mutable Product instance on the heap. To illustrate this, let’s look at how instances of these types are set out in memory.

We create instances of the Purchase type and its properties from Listing 4-1 like this:

```
var existing = new Purchase
{
    Item = new Product { Id = 10990, Price = 12.99m },
    Ordered = DateTime.Parse("2024-02-02"),
    Quantity = 12
};
```

The memory used by the existing variable might look something like Figure 4-1.

![](img/47f0004b0ac0322f285ca59a19bca333_133_0.png)

Figure 4-1: The memory layout of a reference in a struct

Since Purchase is a value type, a variable of type Purchase contains a complete instance in place wherever the variable is declared. In Figure 4-1, the existing identifier is a name representing a memory location containing the values of the three fields of a Purchase type. One of those fields is a backing field for the Item property, whose type is the Product class. As a reference type, the Product instance is allocated on the heap, and the Item property stores a reference to it. The content of the other property values, being value type instances, is stored directly within the existing variable. Now consider what happens when we copy the existing variable in Listing 4-2.

```
var existing = new Purchase
{
    Item = new Product { Id = 10990, Price = 12.99m },
    Ordered = DateTime.Parse("2024-02-02"),
    Quantity = 12
};
--snip--
var copy = existing;
```

Listing 4-2: Copying the value of the existing variable

Because the type of the Item property is a class, only the reference is copied to the new copy variable’s instance, leaving both the existing and copy variables referring to the same Product instance on the heap, as depicted in Figure 4-2.

![](img/47f0004b0ac0322f285ca59a19bca333_134_0.png)

Figure 4-2: The memory layout after copying a struct instance

Having copied existing to copy, we now have two Purchase instances in memory, but the instance data for Item hasn’t been copied. Each Purchase instance has a reference to the same Product on the heap.

## Read-Only Properties vs. Immutable Types

Making the Purchase struct in Listing 4-1 read-only doesn’t protect it from unintended side effects associated with aliasing references, nor does the fact that its Item property has no set accessor. We could still inadvertently modify the object referred to by the Item property because even though Purchase.Item has no set accessor, the Product type it refers to has mutable properties. If we alter a property of the Product instance via the copy variable, that change is visible in the existing variable, as demonstrated in Listing 4-3.

```
var existing = new Purchase
{
    Item = new Product { Id = 10990, Price = 12.99m },
    Ordered = DateTime.Parse("2024-02-02"),
    Quantity = 12
};

var copy = existing;

copy.Item.Price = 14.99;
Assert.That(existing.Item.Price, Is.EqualTo(14.99));
```

Listing 4-3: Altering the state of a Product via a shared reference

Because the properties of the Product type are writable, we can change the instance by using any reference to it. If we make the Product type
