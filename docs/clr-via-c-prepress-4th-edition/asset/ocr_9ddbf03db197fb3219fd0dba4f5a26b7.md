| * | op_Multiply | Multiply |
|---|---|---|
| / | op_Division | Divide |
| % | op_Modulus | Mod |
| & | op_BitwiseAnd | BitwiseAnd |
| \| | op_BitwiseOr | BitwiseOr |
| ^ | op_ExclusiveOr | Xor |
| << | op_LeftShift | LeftShift |
| >> | op_RightShift | RightShift |
| == | op_Equality | Equals |
| != | op_Inequality | Equals |
| < | op_LessThan | Compare |
| > | op_GreaterThan | Compare |
| <= | op_LessThanOrEqual | Compare |
| >= | op_GreaterThanOrEqual | Compare |

The CLR specification defines many additional operators that can be overloaded, but C# does not support these additional operators. Therefore, they are not in mainstream use, so I will not list them here. If you are interested in the complete list, please see the ECMA specifications (www.ecma-international.org/publications/standards/Ecma-335.htm) for the Common Language Infrastructure (CLI), Partition I, Concepts and Architecture, Sections 10.3.1 (unary operators) and 10.3.2 (binary operators).

**Note** If you examine the core numeric types (Int32, Int64, UInt32, and so on) in the Framework Class Library (FCL), you'll see that they don't define any operator overload methods. The reason they don't is that compilers look specifically for operations on these primitive types and emit IL instructions that directly manipulate instances of these types. If the types were to offer methods and if compilers were to emit code to call these methods, a run-time performance cost would be associated with the method call. Plus, the method would ultimately have to execute some IL instructions to perform the expected operation anyway. This is why the core FCL types don't define any operator overload methods. Here's what this means to you: If the programming language you're using doesn't support one of the core FCL types, you won't be able to perform any operations on instances of that type.