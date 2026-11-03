# 14.2 Storage Classes

In addition to data type, each variable has one more attribute known as storage class. The proper use of storage classes makes our program efficient and fast. In larger multifile programs the knowledge of storage classes is indispensable. We can specify a storage class while declaring a variable. The general syntax is-
storage_class datatype variable_name;

+   There are four types of storage classes-
+   1. Automatic
+   2. External
+   3. Static
+   4. Register

The keywords auto, static, register, extern are used for these storage classes. So we may write declaration statements like this-
auto int x, y;
static float d;
register int z;

When the storage class specifier is not present in the declaration, compiler assumes a default storage class based on the place of declaration.

A storage class decides about these four aspects of a variable-

+   (1) Lifetime - Time between the creation and destruction of a variable.
+   (2) Scope - Locations where the variable is available for use.
+   (3) Initial value - Default value taken by an uninitialized variable.
+   (4) Place of storage - Place in memory where the storage is allocated for the variable.

Now we'll discuss all these storage classes one by one in detail.

# 14.2.1 Automatic

All the variables declared inside a block/function without any storage class specifier are called automatic variables. We may also use the keyword auto to declare automatic variables, although this is generally not done. The following two declaration statements are equivalent and both declare a and b to be automatic variables of type int.

```
func()
{
    int a,b;
    ....
}
```

```
func()
{
    auto int a,b;
    .......
}
```

The uninitialized automatic variables initially contain garbage value. The scope of these variables is inside the function or block in which they are declared and they can't be used in any other function/block.