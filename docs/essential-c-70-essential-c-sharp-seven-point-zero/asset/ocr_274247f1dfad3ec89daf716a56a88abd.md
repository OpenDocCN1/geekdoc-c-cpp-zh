# All Classes Derive from System.Object

Given any class, whether a custom class or one built into the system, the methods shown in Table 7.2 will be defined.

**TABLE 7.2: Members of System.\object**

| Method Name | Description |
| :--- | :--- |
| public virtual bool Equals(object o) | Returns true if the object supplied as a parameter is equal in value, not necessarily in reference, to the instance. |
| public virtual int GetHashCode() | Returns an integer corresponding to an evenly spread hash code. This is useful for collections such as HashTable collections. |
| public Type GetType() | Returns an object of type System.Type corresponding to the type of the object instance. |
| public static bool ReferenceEquals(object a, object b) | Returns true if the two supplied parameters refer to the same object. |
| public virtual string ToString() | Returns a string representation of the object instance. |
| public virtual void Finalize() | An alias for the destructor; informs the object to prepare for termination. C# prevents you from calling this method directly. |
| protected object MemberwiseClone() | Clones the object in question by performing a shallow copy; references are copied, but not the data within a referenced type. |

All of the methods listed in Table 7.2 appear on all objects through inheritance; all classes derive (either directly or via an inheritance chain) from object. Even literals include these methods, enabling somewhat peculiar-looking code such as this:

```
Console.WriteLine( 42.ToString() );
```

Even class definitions that don't have any explicit derivation from object derive from object anyway. The two declarations for PdaItem in Listing 7.21, therefore, result in identical Cil.