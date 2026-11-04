other type. Also, since arrays are implemented as objects, a variable of type object can also refer to any array. Technically, the C# name object is just another name for System.Object, which is part of the .NET Framework class library.

The object class defines the methods shown in Table 11-1, which means that they are available in every object.

A few of these methods warrant some additional explanation. By default, the Equals(object) method determines if the invoking object refers to the same object as the one referred to by the argument. (That is, it determines if the two references are the same.) It returns true if the objects are the same, and false otherwise. You can override this method in classes that you create. Doing so allows you to define what equality means relative to a class. For example, you could define Equals(object) so that it compares the contents of two objects for equality. The Equals(object, object) method invokes Equals(object) to compute its result.

The GetHashCode() method returns a hash code associated with the invoking object. This hash code can be used with any algorithm that employs hashing as a means of accessing stored objects.

As mentioned in Chapter 9, if you overload the == operator, then you will usually need to override Equals(object) and GetHashCode() because most of the time you will want the == operator and the Equals(object) methods to function the same. When Equals() is overridden, you should also override GetHashCode(), so that the two methods are compatible.

The ToString() method returns a string that contains a description of the object on which it is called. Also, this method is automatically called when an object is output using

| Method | Purpose |
|---|---|
| public virtual bool Equals(object ob) | Determines whether the invoking object is the same as the one referred to by ob. |
| public static bool Equals(object ob1, object ob2) | Determines whether ob1 is the same as ob2. |
| protected virtual Finalize() | Performs shutdown actions prior to garbage collection. In C#, Finalize() is accessed through a destructor. |
| public virtual int GetHashCode() | Returns the hash code associated with the invoking object. |
| public Type GetType() | Obtains the type of an object at runtime. |
| protected object MemberwiseClone() | Makes a "shallow copy" of the object. This is one in which the members are copied, but objects referred to by members are not. |
| public static bool ReferenceEquals(object ob1, object ob2) | Determines whether ob1 and ob2 refer to the same object. |
| public virtual string ToString() | Returns a string that describes the object. |