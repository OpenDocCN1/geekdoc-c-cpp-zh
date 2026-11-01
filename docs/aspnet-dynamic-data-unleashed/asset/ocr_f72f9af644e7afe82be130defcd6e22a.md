Notice that the type of the Customers property is now the IObjectSet<T> interface and not the concrete class, ObjectSet<T>. The property getter no longer returns the built-in object created by the CreateObjectSet method provided by the Entity Framework. Instead, it returns an instance of the FilteredObjectSet, a custom class created to modify the default Customers query. This class reimplements the IObjectSet<T> interface by wrapping an original ObjectSet<T> instance, delegating most of the properties and methods to the original and augmenting the functionality of the IQueryable properties based on the CustomQueryAttribute. In other words, the FilteredObjectSet class implements the Decorator pattern to add row-level security to the built-in ObjectSet class. Listing 14.2 shows its entire source code with important areas highlighted in bold.

# LISTING 14.2 FilteredObjectSet Implementation

```
using System;
using System.Collections;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data.Objects;
using System.Linq;
using System.Linq.Expressions;
using Unleashed.DataAnnotations;

namespace DataModel
{
    public class FilteredObjectSet<T> : IObjectSet<T> where T : class
    {
        private static readonly CustomQueryAttribute customQueryAttribute = TypeDescriptor.GetAttributes(typeof(T)).OfType<CustomQueryAttribute>().FirstOrDefault();

        private readonly ObjectSet<T> original;

        public FilteredObjectSet(ObjectSet<T> original)
        {
            this.original = original;
        }

        public IEnumerator<T> GetEnumerator()
        {
            return ((IEnumerable<T>)this.original).GetEnumerator();
        }

        IEnumerator IEnumerable.GetEnumerator()
        {
            return this.GetEnumerator();
        }
```