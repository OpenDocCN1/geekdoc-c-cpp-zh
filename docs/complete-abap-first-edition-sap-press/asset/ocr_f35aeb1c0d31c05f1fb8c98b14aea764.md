The base class for all exception classes is `CX_ROOT`, which implements the `IF_MESSAGE` and `IF_SERIALIZABLE_OBJECT` interfaces. The `IF_MESSAGE` interface contains the `GET_TEXT` and `GET_LONGTEXT` methods, which allow you to extract the error message. The `IF_SERIALIZABLE_OBJECT` interface is used for *object serialization*, a process in which the object is converted into a serialization format (e.g., XML, CSV) that can be transmitted to create a clone of the object in the same system or another system. The `IF_SERIALIZABLE_OBJECT` interface should be implemented if the exception object needs to be serialized. The `CX_ROOT` class also implements another method, `GET_SOURCE_POSITION`, which returns the position in the source code that caused the error.

When catching class-based exceptions, the exception information is captured by an object that is an instance of a class that inherits from one of three global abstract classes: `CX_STATIC_CHECK`, `CX_DYNAMIC_CHECK`, or `CX_NO_CHECK`. These three global abstract classes are in turn subclasses of `CX_ROOT`. For example, in Listing 9.5, we can define the `R_ER` reference object as an instance of the `CX_ROOT` class instead of the `CX_SY_ZERODIVIDE` class and still be able to catch the exception as shown in Listing 9.6. However, doing so will make the error logic generic and miss any specific exception handling details maintained in the specific exception class.

```
DATA r_ex TYPE REF TO cx_root.
TRY.
  v_unit_value = v_total_value / v_quantity.
CATCH cx_sy_zerodivide INTO r_ex.
  WRITE / 'Error Short Text:' r_ex->get_text( ).
  WRITE / 'Error long Text:' r_ex->get_longtext( ).
ENDTRY.
```

**Listing 9.6** Using CX_ROOT Instance

As noted, when defining a custom exception class, it should inherit from one of three classes:

+   - `CX_STATIC_CHECK`
+   
+     If an exception class that's a subclass of `CX_STATIC_CHECK` is raised in a function module or method, it should be either defined in the signature (parameter interface) or caught in the procedure within a TRY block. Otherwise, a warning message is shown by the syntax checker.