Even if you do not need access to command-line arguments, you can still use the version of the Main() method header that references them. You should use this version if your instructor or supervisor indicates you should follow this convention.

# Writing a Main() Method with an Integer Return Type

Some programmers prefer to write Main() method headers that have a return type of int instead of void. If you use this form, the last statement in the Main() method must be a return statement that returns an integer. By convention, a return value of 0 means that an application ended without error. The value might be used by your operating system or another program that uses your program. In particular, C++ programmers prefer the version of Main() that returns an int because conventionally they write their methods with an int type.

If you do not need to use a return value from a Main() method, you can still use the version of the Main() method header that includes a return value. You should use this version if your instructor or supervisor indicates you should follow this convention.

# Writing a Main() Method with public Access

Some programmers prefer to write Main() method headers with public access rather than private, which is the default access when no qualifier is listed. In Java, programmers might prefer using public because the style is conventional for them. If a class Main()'s method is public, it can be called from another class using its fully qualified name. You rarely want to do this, C# programmers often omit the Main() method's access specifier, making it private by default.

![](bbox=[0.137, 0.647, 0.862, 0.833])