property. Furthermore, by invoking each property on each object, the list control could populate each row and column with the data contained in the object, even though the data type of the object is unknown at compile time. XmlSerializer, ValueType, and DataBinder are a few of the classes in the framework that use reflection for portions of their implementation as well.

# Accessing Metadata Using System.Type

The key to reading a type's metadata is to obtain an instance of System.Type that represents the target type instance. System.Type provides all the methods for retrieving the information about a type. You can use it to answer questions such as the following,

+   - What is the type's name (Type.Name)?
+   - Is the type public (Type.IsPublic)?
+   - What is the type's base type (Type.BaseType)?
+   - Does the type support any interfaces (Type.GetInterfaces())?
+   - Which assembly is the type defined in (Type.Assembly)?
+   - What are a type's properties, methods, fields, and so on (Type.GetProperties(), Type.GetMethods(), Type.GetFields(), and so on)?
+   - What attributes decorate a type (Type.GetCustomAttributes())?

There are more such members, but in summary, they all provide information about a particular type. The key is to obtain a reference to a type's Type object, and the two primary ways to do this are through object.GetType() and typeof(). Note that the GetMethods() call does not return extension methods. They are available only as static members on the implementing type.

# GetType()

object includes a GetType() member, and therefore, all types include this function. You call GetType() to retrieve an instance of System.Type corresponding to the original object. Listing 17.1 demonstrates this, using a Type instance from DateTime. Output 17.1 shows the results.