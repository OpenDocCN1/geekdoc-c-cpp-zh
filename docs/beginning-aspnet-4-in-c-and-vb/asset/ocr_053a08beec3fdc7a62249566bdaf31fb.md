```
[DataServiceKey("Id")]
public class Category
{
    public int Id { get; set; }
    public string Name { get; set; }

    public Category() { }
    public Category(int id, string name)
    {
        this.Id = id;
        this.Name = name;
    }
}
```

code snippet DataServicesHost/Category.cs

```
[DataServiceKey("Id")]
public class Menu
{
    public int Id { get; set; }
    public string Name { get; set; }
    public decimal Price { get; set; }
    public Category Category { get; set; }

    public Menu() { }
    public Menu(int id, string name, decimal price, Category category)
    {
        this.Id = id;
        this.Name = name;
        this.Price = price;
        this.Category = category;
    }
}
```

code snippet DataServicesHost/Menu.cs

The class MenuCard manages the collections of Menu and Category items. It contains a list of Menu and Category items that can be iterated from the public Menus and Categories properties. This class implements a singleton pattern, so only one list of each exists.

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace Wrox.ProCSharp.DataServices
{
    public class MenuCard
    {
        private static object sync = new object();
        private static MenuCard menuCard;
        public static MenuCard Instance
        {
            get
            {
                lock (sync)
                {
                    if (menuCard == null)
                    {
                        menuCard = new MenuCard();
                    }
                }
                return menuCard;
            }
        }
```