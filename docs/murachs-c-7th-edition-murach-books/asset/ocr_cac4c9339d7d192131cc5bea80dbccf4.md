# A class that works with a binary file

```
```csharp
using System;
using System.IO;
using System.Collections.Generic;

namespace ProductMaintenance
{
    public class ProductDB
    {
        private const string dir = @"C:\C#\Files\";
        private const string path = dir + "Products.dat";

        public static List<Product> GetProducts()
        {
            if (!Directory.Exists(dir))
                Directory.CreateDirectory(dir);

            using BinaryReader binaryIn =
                new BinaryReader(
                new FileStream(path, FileMode.OpenOrCreate, FileAccess.Read));

            List<Product> products = new List<Product>();
            while (binaryIn.PeekChar() != -1)
            {
                Product product = new Product();
                product.Code = binaryIn.ReadString();
                product.Description = binaryIn.ReadString();
                product.Price = binaryIn.ReadDecimal();
                products.Add(product);
            }

            return products;
        }

        public static void SaveProducts(List<Product> products)
        {
            using BinaryWriter binaryOut =
                new BinaryWriter(
                new FileStream(path, FileMode.Create, FileAccess.Write));

            foreach (Product product in products)
            {
                binaryOut.Write(product.Code);
                binaryOut.Write(product.Description);
                binaryOut.Write(product.Price);
            }
        }
    }
}
```
```

Figure 17-11    A class that works with a binary file