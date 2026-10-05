# A class that works with a binary file

```
using System;
using System.IO;
using System.Collections.Generic;
```

```
namespace ProductMaintenance
{
    public class ProductDB
    {
        private const string dir = @"C:\2010\Files\";
        private const string path = dir + "Products.dat";

        public static List<Product> GetProducts()
        {
            if (!Directory.Exists(dir))
                Directory.CreateDirectory(dir);

            BinaryReader binaryIn = new BinaryReader(path, FileMode.OpenOrCreate, FileAccess.Read);
            List<Product> products = new List<Product>();
            while (binaryIn.PeekChar() != -1)
            {
                Product product = new Product();
                product.Code = binaryIn.ReadString();
                product.Description = binaryIn.ReadString();
                product.Price = binaryIn.ReadDecimal();
                products.Add(product);
            }
            binaryIn.Close();
            return products;
        }

        public static void SaveProducts(List<Product> products)
        {
            BinaryWriter binaryOut = new BinaryWriter(path, FileMode.Create, FileAccess.Write);

            foreach (Product product in products)
            {
                binaryOut.Write(product.Code);
                binaryOut.Write(product.Description);
                binaryOut.Write(product.Price);
            }
            binaryOut.Close();
        }
    }
}
```

Figure 21-10 A class that works with a binary file