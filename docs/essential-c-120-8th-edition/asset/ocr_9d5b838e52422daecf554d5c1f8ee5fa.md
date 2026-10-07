# All Classes Derive from System.Object

```
Address: 221B Baker Street, London, England

Subject: Soccer tournament
Start: 7/18/2008 12:00:00 AM
End: 7/19/2008 12:00:00 AM
Location: Estádio da Machava
-----------------
FirstName: Hercule
LastName: Poirot
Address: Apt 56B, Whitehaven Mansions, Sandhurst Sq, London
```

In this way, you can call the method on the base class, but the implementation is specific to the derived class. Output 7.5 shows that the List() method from Listing 7.18 is able to successfully display both Contacts and Addresses, and display them in a way tailored to each. The invocation of the abstract GetSummary() method actually invokes the overriding method specific to the instance.

# All Classes Derive from System.Object

Given any class, whether a custom class or one built into the system, the methods shown in Table 7.2 will be defined.

Table 7.2: Members of System.Object
| Method Name | Description |
| --- | --- |
| public virtual Equals(object o) | Returns true if the object supplied as a parameter is equal in value, not necessarily in reference, to the instance. |
| public virtual int GetHashCode() | Returns an integer corresponding to an evenly spread hash code. This is useful for collections such as HashTable collections. |
| public Type GetType() | Returns an object of type System.Type corresponding to the type of the object instance. |
| public static bool ReferenceEquals(object a, object b) | Returns true if the two supplied parameters refer to the same object. |
| public virtual string ToString() | Returns a string representation of the object instance. |