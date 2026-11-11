returns the class object for the class that defines this constructor, method, or field.

+   - `Class[] getExceptionTypes()` (in `Constructor` and `Method` classes)
+   
+     returns an array of class objects that represent the types of the exceptions thrown by the method.
+   
+   - `int getModifiers()`
+   
+     returns an integer that describes the modifiers of this constructor, method, or field. Use the methods in the `Modifier` class to analyze the return value.
+   
+   - `String getName()`
+   
+     returns a string that is the name of the constructor, method, or field.
+   
+   - `Class[] getParameterTypes()` (in `Constructor` and `Method` classes)
+   
+     returns an array of class objects that represent the types of the parameters.
+   
+   - `Class getReturnType()` (in `Method` class)
+   
+     returns a class object that represents the return type.

# ### java.lang.reflect.RecordComponent 16

+   - `String getName()`
+     `Class<?> getType()`
+   
+     get the name and type of this record component
+   
+   - `Method getAccessor()`
+   
+     returns the `Method` object for accessing this record component

# ### java.lang.reflect.Modifier 1.1