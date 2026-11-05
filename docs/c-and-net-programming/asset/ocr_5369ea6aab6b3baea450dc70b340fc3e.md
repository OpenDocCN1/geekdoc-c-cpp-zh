# 12.5 Hashtable Class

# Properties of the Hashtable Class

| Property | Description |
|---|---|
| Count | Gets the number of key-and-value pairs contained in the Hashtable. |
| IsFixedSize | Gets a value indicating whether the Hashtable has a fixed size. |
| IsReadOnly | Gets a value indicating whether the Hashtable is read-only. |
| Item | Gets or sets the value associated with the specified key. |
| Keys | Gets an ICollection containing the keys in the Hashtable. |
| Values | Gets an ICollection containing the values in the Hashtable. |

# Methods of the Hashtable Class

| Sr.No. | Method |
|---|---|
| 1 | public virtual void Add(object key, object value);
Adds an element with the specified key and value into the Hashtable. |
| 2 | public virtual void Clear();
Removes all elements from the Hashtable. |
| 3 | public virtual bool ContainsKey(object key);
Determines whether the Hashtable contains a specific key. |
| 4 | public virtual bool ContainsValue(object value);
Determines whether the Hashtable contains a specific value. |
| 5 | public virtual void Remove(object key);
Removes the element with the specified key from the Hashtable. |

# Example

The following example demonstrates the concept:

```
using System;
using System.Collections;

namespace CollectionsApps
{
class Program
```