| Construct | Example | Description |
|---|---|---|
| Property access | P | The get accessor of the property P in the containing class or struct is invoked. A compile-time error occurs if P is write-only. If P is not static, the instance expression is this. |
|  | P = value | The set accessor of the property P in the containing class or struct is invoked with the argument list (value). A compile-time error occurs if P is read-only. If P is not static, the instance expression is this. |
|  | T.P | The get accessor of the property P in the class or struct T is invoked. A compile-time error occurs if P is not static or if P is write-only. |
|  | T.P = value | The set accessor of the property P in the class or struct T is invoked with the argument list (value). A compile-time error occurs if P is not static or if P is read-only. |
|  | e.P | The get accessor of the property P in the class, struct, or interface given by the type of e is invoked with the instance expression e. A binding-time error occurs if P is static or if P is write-only. |
|  | e.P = value | The set accessor of the property P in the class, struct, or interface given by the type of e is invoked with the instance expression e and the argument list (value). A binding-time error occurs if P is static or if P is read-only. |