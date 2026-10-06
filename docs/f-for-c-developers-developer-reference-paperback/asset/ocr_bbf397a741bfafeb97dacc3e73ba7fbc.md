# Using Exceptions with F#

Although the exception is not an F# specific type, F#'s exception definition can be very different from a C# exception definition. Listing 6-117 shows how to use F# reflection on exceptions—specifically, how to check the exception, get exception fields, and get exception field values.

**LISTING 6-117** Using F# reflection on an exception

```
Source code
open Microsoft.CSharp.Reflection

exception MyException of int * int

let ex = MyException(1, 2)

// check if it is an exception representation
FSharpType.IsExceptionRepresentation(ex.GetType())

// get exception fields
FSharpType.GetExceptionFields(ex.GetType())

// get exception field values
FSharpValue.GetExceptionFields(ex)

Execution result
val it : bool = true
>
val : System.Reflection.PropertyInfo [] = [[Int32 Data0 =
 {Attributes = None;
  CanRead = true;
  CanWrite = false;
  CustomAttributes = seq
 [[Microsoft.CSharp.Core.CompilationMappingAttribute(Microsoft.CSharp.SourceConstructFlags(4,Int32(0))];
  DeclaringType = FSI_0046+MyException;
  TestMethod = Int32 get_Data0();
  IsSpecialName = false;
  MemberType = Property;
  MetadataToken = 385876082;
  Module = FSI-ASSEMBLY;
  Name = "Data0";
  Property = System.Int32;
  ReflectedType = FSI_0046+MyException;
  SetMethod = null];
Int32 Data1
 {Attributes = None;
  CanRead = true;]]
```