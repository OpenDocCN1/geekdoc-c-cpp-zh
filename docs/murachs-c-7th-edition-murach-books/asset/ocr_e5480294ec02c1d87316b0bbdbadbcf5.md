# A method that uses the using statement

```
public static void SaveProducts(List<Product> products)
{
using (StreamWriter textOut =
new StreamWriter(
new FileStream(path, FileMode.Create, FileAccess.Write)))
{
foreach (Product product in products)
{
textOut.Write(product.Code + "|");
textOut.Write(product.Description + "|");
textOut.WriteLine(product.Price);
}
}
}
```

# The same method with a using declaration

```
public static void SaveProducts(List<Product> products)
{
using StreamWriter textOut =
new StreamWriter(
new FileStream(path, FileMode.Create, FileAccess.Write));

foreach (Product product in products)
{
textOut.Write(product.Code + "|");
textOut.Write(product.Description + "|");
textOut.WriteLine(product.Price);
}
}
```

# Description

+   - The using statement causes any resources used by an object to be released from memory when the object goes out of scope. In addition, before the resources are released, the object is closed if necessary.
+   - To use the using statement, you code the using keyword, followed by the object declaration enclosed in parentheses and the block of code that uses the object. Then, the resources used by the object will be released when the block ends.
+   - C# 8.0 introduced the using declaration, which can be used to release the resources used by an object at the end of the scope in which it’s declared.
+   - To use a using declaration, you simply code the using keyword at the beginning of an object declaration.
+   - An object that is declared with a using statement or using declaration is read-only and can’t be modified.

![](bbox=[0.05, 0.96, 0.95, 0.99])