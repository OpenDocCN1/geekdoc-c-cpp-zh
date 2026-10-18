+   153. The qualifier **const** appended to function prototype indicates that the function does not modify any of the data members. A **const** member function can be used by **const** objects of the class.
+   
+   154. The client interface to a class object occurs in the **public** section of the class definition.
+   
+   155. Any member defined in any section — whether **public**, **protected**, or **private**— is accessible to all of the other members of its class.
+   
+   156. Members of a **protected** section are intended to be used by a class derived from the class.
+   
+   157. Data members are normally declared in a **private**. By restricting outside access to the data members in a class, it is easier to ensure the integrity and consistency of their values.
+   
+   158. Members of **private** section of a class are intended to be used only by the members of that class.
+   
+   159. An & in the return type for a function or operator indicates that a reference return is being performed. In a reference return, a reference to the actual object in the return expression rather than a copy is returned. The scope of the returned object should not be local to the invoked function or operator.
+   
+   160. When creating a **friend** function, use the keyword friend in the prototype in the class definition, but do not use this keyword in the actual function definition. Friend functions are defined outside the class definition.
+   
+   161. Friend functions have access to the private and protected members of a class.
+   
+   162. An operator can be overloaded many times using distinct signatures.
+   
+   163. If we want to overload a binary operator with two different types of operands with non class as the first operand, we must use a **friend** function to define the operator overloading.