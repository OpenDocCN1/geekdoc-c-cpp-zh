# # Example

```
```csharp
//illustrating use of reflection to inspects a class and to display the metadata information
//dynamically.
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;

namespace ReflectionDemo
{
    public class Book
    {
        //string Title;
        public string Title
        {
            get
            {
                return Title;
            }
            set
            {
                Title = val;
            }
        }
        public Book()
        {
        }
        public Book(string t)
        {
            this.Title = t;
        }
        public void Show()
        {
        }

        public string val { get; set; }
    }
    public class ApplyReflection
    {
        public static void MetadataDetails(Type tp)
        {
            Console.WriteLine("Class " + tp);
            Console.WriteLine();
```
```