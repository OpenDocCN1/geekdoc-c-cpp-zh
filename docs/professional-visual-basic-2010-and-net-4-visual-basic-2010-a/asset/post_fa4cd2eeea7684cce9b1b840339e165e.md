
With SQL Server 2005 and later, you can create UDTs using Visual Basic. In addition to the normal benefits of user-defined types, UDTs written in Visual Basic have another benefit — they may also provide functionality in the form of methods, which means that you can extend the functionality of your database by providing these methods.

UDTs written using Visual Basic are implemented as structures or classes. Since Visual Studio defaults to creating UDTs as structures, this will be assumed here, but keep in mind that you can create them as classes as well. The properties or fields of the structure become the subtypes of the UDT. Public methods are also accessible, just as they would be in a Visual Basic application.

In addition to the normal code used when writing structures, you must also implement other items to make your UDT work with SQL Server. First, your structure should have the attribute `Microsoft.SqlServer.Server.SqlUserDefinedType`. This attribute identifies the structure as being a SQL Server UDT. In addition, marking the class with the `Serializable` attribute is highly recommended. The `SqlUserDefinedType` attribute has a number of parameters that provide information affecting how SQL Server works with the type. These parameters are described in Table 12-3.

### TABLE 12-3: SqlUserDefinedType Attribute Parameters

| PARAMETER | VALUE | DESCRIPTION |
|---|---|---|
| Format | Native or UserDefined | Identifies the serialization format. If you use Native (the default when you create your UDT with Visual Studio), then it uses the SQL Server serialization model. If you set it to UserDefined, you must also implement `Microsoft.SqlServer.Server.IBinarySerialize`. This interface includes methods for reading and writing your data type. Generally, using Native is safe enough unless your data type requires special handling to avoid saving it incorrectly. For example, if you were storing a media stream, you would likely set it as UserDefined to avoid writing the stream incorrectly. |
| IsByteOrdered | Boolean | True if the data is stored in byte order, false if it is stored using some other order. If this is true, then you can use the default comparison operators with the type, as well as use it as a primary key. The capability to compare two values is a great indicator of how you should use this parameter. If it is possible to define one instance of this UDT as being larger than another, then `IsByteOrdered` is likely true. If it is not, such as with a latitude value, then `IsByteOrdered` is false. |
| IsFixedLength | Boolean | This should be set to true if all instances of this type are the same size. If the UDT includes only fixed-size elements, such as int, double, or char (20), then this is true. If it includes variable-size elements, such as varchar (50) or text, then it should be false. This is a marker to enable optimizations by the SQL Server query processor. |
| ValidationMethodName | String | Name of a method to be used to validate the data in the UDT. This method is used when loading the UDT, and should return true if the data is valid. |
| MaxByteSize | Integer, with a maximum of 8000 | Defines the maximum size of the UDT, in bytes |

In addition to this attribute, each user-defined type also needs to implement the shared method `Parse`, and the instance method `ToString`. These methods enable conversion between your new data type and the interim format, `SqlString`. Finally, you should also implement `INullable` in your structure, although this is not a requirement. This interface requires the addition of the `IsNull` property, which enables your UDT to deal with null values, either stored in the database or passed from the client.

> If you are using Visual Studio to create your UDTs, then it’s best to create and debug all of your UDTs before you begin to use them, especially if you need to use them in any table columns. This is because Visual Basic drops all of the objects you create in a SQL Server project when deploying the project. If you have any tables that use any user-defined types, then you will be unable to drop the UDT, and therefore deploy the changes you’ve made. If you need to make changes, you may receive an error similar to “Cannot drop type ‘Location’ because it is currently in use.” This error causes the deploy step of your project to fail. If this happens, then change the column type or temporarily drop the table. You can then redeploy the UDT as needed. Don’t forget to change the column back, or recreate the table.

While you can write code that integrates with SQL Server using any DLL, Visual Studio provides the Visual Basic SQL CLR Database Project (see Figure 12-19). This project type generates a DLL but also connects the DLL to the database.

![](img/d99870e80390742f93963da7be0b2e61_485_0.png)

### FIGURE 12-19

> SQL Server 2008 only supports .NET 4 assemblies if you have installed the cumulative update 5 for Service Pack 1.

When you create a new SQL Server Project, Visual Studio prompts you to identify the database that will host the DLL. At this point, you can either select an existing database connection or create a new one. For the sample project, create a new database called FooStore. Visual Studio also asks whether you want to enable SQL/CLR debugging on the connection. Typically, you will want to enable this on development servers, but keep in mind that when debugging, the server is limited to the single connection. Once the project is created, you can add the various database types via the Project menu. Deploying the project (via the Deploy option on the Build menu) loads the created DLL into the database. You can confirm that it is loaded by looking at the Assemblies folder in the Server Explorer (see Figure 12-20).

![](img/d99870e80390742f93963da7be0b2e61_486_0.png)

The following code example shows a simple `Location` user-defined type written in Visual Basic. This type identifies a geographic location. We will use it throughout the remainder of the chapter to track the location of customers and stores. The `Location` type has two main properties: `Latitude` and `Longitude`. Create this file by selecting Add User-defined Type from the Project menu.

```vb
Imports System
Imports System.Data
Imports System.Data.SqlClient
Imports System.Data.SqlTypes
Imports Microsoft.SqlServer.Server
<Serializable()> _
<Microsoft.SqlServer.Server.SqlUserDefinedType(Format.Native)> _
Public Structure Location
    Implements INullable
    Public ReadOnly Property IsNull() As Boolean Implements INullable.IsNull
        Get
            If Me.Latitude = Double.NaN OrElse Me.Longitude = Double.NaN Then
                _isNull = True
            Else
                _isNull = False
            End If
            Return _isNull
        End Get
    End Property
    Public Shared ReadOnly Property Null As Location
        Get
            Dim result As Location = New Location
            result._isNull = True
            result.Latitude = Double.NaN
            result.Longitude = Double.NaN
            Return result
        End Get
    End Property
    Public Overrides Function ToString() As String
        Return String.Format("({0}, {1})", Latitude, Longitude)
    End Function
    Public Shared Function Parse(ByVal s As SqlString) As Location
        If s.IsNull Then
            Return Null
        End If
        Dim result As Location = New Location
        Dim temp() As String = s.Value.Split(CChar(","))
        If (temp.Length > 1) Then
            result.Latitude = Double.Parse(temp(0))
            result.Longitude = Double.Parse(temp(1))
        End If
        Return result
    End Function
    Public Function Distance(ByVal loc As Location) As Double
        Dim result As Double
        Dim temp As Double
        Dim deltaLat As Double
        Dim deltaLong As Double
        Const EARTH_RADIUS As Integer = 6378 'kilometers
        Dim lat1 As Double
        Dim lat2 As Double
        Dim long1 As Double
        Dim long2 As Double
        'convert to radians
        lat1 = Me.Latitude * Math.PI / 180
        long1 = Me.Longitude * Math.PI / 180
        lat2 = loc.Latitude * Math.PI / 180
        long2 = loc.Longitude * Math.PI / 180
        'formula from http://mathforum.org/library/drmath/view/51711.html
        deltaLong = long2 - long1
        deltaLat = lat2 - lat1
        temp = (Math.Sin(deltaLat / 2)) ^ 2 + _
            Math.Cos(lat1) * Math.Cos(lat2) * (Math.Sin(deltaLong / 2)) ^ 2
        temp = 2 * Math.Atan2(Math.Sqrt(temp), Math.Sqrt(1 - temp))
        result = EARTH_RADIUS * temp
        Return result
    End Function

    Private _lat As Double
    Private _long As Double
    Private _isNull As Boolean
    Public Property Latitude() As Double
        Get
            Return _lat
        End Get
        Set(ByVal value As Double)
            _lat = value
        End Set
    End Property
    Public Property Longitude() As Double
        Get
            Return _long
        End Get
        Set(ByVal value As Double)
            _long = value
        End Set
    End Property
End Structure
```

Code snippet from FooStore

In addition to the `Latitude` and `Longitude` properties, the `Location` type also defines a `Distance` method. This is used to identify the distance between two locations. It uses the formula for calculating the distance between two points on a sphere to calculate the distance. This formula is clearly described at the “Ask Dr. Math” forum (see http://mathforum.org/library/drmath/view/51879.html). As the Earth is not a perfect sphere, this calculation is only an estimate, but it should be close enough for our needs.

Look at the properties for the project; on the Database tab for the properties, ensure that the connection string has been set to the FooStore database. For now, select Safe for the Permission Level. Right-click the project in the Solution Explorer and select Deploy; this will build the project and copy the DLL to the database.

Now that you have created the `Location` type, you can use it in the definition of a table. Here we will create part of an e-commerce application to demonstrate the use of `Location` and other SQL Server features.
