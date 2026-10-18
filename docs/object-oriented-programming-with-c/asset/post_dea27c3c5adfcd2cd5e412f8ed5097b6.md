
- 119. It is a good practice to declare the size of an array as a constant using the qualifier **const**.

- 120. C++ supports two types of parameters, namely, value parameters and reference parameters.

- 121. When a parameter is passed by value, a copy of the variable is passed to the **called** function. Any modifications made to the parameter by the **called** function change the copy, not the original variable.

- 122. When a reference parameter is used, instead of passing a copy of the variable, a reference to the original variable is passed. Any modifications made to the parameter by the **called** function change the original variable.

- 123. When an **iostream** object is passed to a function, either an extraction or an insertion operation implicitly modifies the stream. Thus, stream objects should be passed as reference.

- 124. A reason to use a reference parameter is for efficiency. When a class object is passed by value, a copy of the object is passed. If the object is large, making a copy of it can be expensive in terms of execution time and memory space. Thus objects that are large, or objects whose size is not known are often passed by reference. We can ensure that the objects are not modified by using the **const** modifier.

- 125. A **const** modifier applied to a parameter declaration indicates that the function may not change the object. If the function attempts to modify the object, the compiler will report a compilation error.

- 126. A reference variable must be initialized when it is declared.

- 127. When you are returning an address from a function, never return the address of a local variable though, syntactically, this is acceptable.

- 128. If a function call argument does not match the type of a corresponding reference parameter, C++ creates an anonymous variable of the correct type, assigns the value of the argument to it and causes the reference parameter to refer to the variable.

- 129. A function that returns a reference is actually an alias for the ‘referred-to’ variable.

- 130. We can assign a value to a C++ function, if the function returns a reference to a variable. The value is assigned to the referred-to variable.

- 131. C++’s default parameter mechanism provides the ability to define a function so that a parameter gets a default value if a call to the function does not give a value for that parameter.

- 132. Function overloading occurs when two or more functions have the same name.

- 133. The compiler resolves overloaded function calls by calling the function whose parameter list best matches that of the call.

- 134. Casting expressions provide a facility to explicitly convert one type to another.

- 135. A cast expression is useful when the programmer wants to force the compiler to perform a particular type of operation such as floating-point division rather than integer division.

- 136. A cast expression is useful for converting the values that library functions return to the appropriate type. This makes it clear to other programmers that the conversion was intended.

- 137. An inline function must be defined before it is called.

- 138. An inline function reduces the function call overhead. Small functions are best declared inline within a class.

- 139. In a multiple-file program, you can define an external variable in one and only one file. All the other files using that variable have to declare it with the keyword extern.

- 140. An abstract data type (ADT) is a well-defined and complete data abstraction that uses the principle of information-hiding.

- 141. An ADT allows the creation and manipulation of objects in a natural manner.

- 142. If a function or operator can be defined such that it is not a member of the class, then do not make it a member. This practice makes a nonmember function or operator generally independent of changes to the class’s implementation.

- 143. In C++, an abstract data type is implemented using classes, functions, and operators.

- 144. Constructors initialize objects of the class type. It is a standard practice to ensure that every object has all of its data members appropriately initialized.

- 145. A default constructor is a constructor that requires no parameters.

- 146. A copy constructor initializes a new object to be a duplicate of a previously defined source object. If a class does not define a copy constructor, the compiler automatically supplies a version.

- 147. A member assignment operator copies a source object to the invoking target object in an assignment statement. If a class does not define a member assignment operator, the compiler automatically supplies a version.

- 148. When we call a member function, it uses the data members of the object used to invoke the member function.

- 149. A class constructor, if defined, is called whenever a program creates an object of that class.

- 150. When we create constructors for a class, we must provide a default constructor to create uninitialized objects.

- 151. When we assign one object to another of the same class, C++ copies the contents of each data member of the source object to the corresponding member of the target object.

- 152. A member function operates upon the object used to invoke it, while a friend function operates upon the objects passed to it as arguments.

- 153. The qualifier **const** appended to a function prototype indicates that the function does not modify any of the data members. A **const** member function can be used by **const** objects of the class.

- 154. The client interface to a class object occurs in the **public** section of the class definition.

- 155. Any member defined in any section — whether **public**, **protected**, or **private** — is accessible to all of the other members of its class.

- 156. Members of a **protected** section are intended to be used by a class derived from the class.

- 157. Data members are normally declared in a **private** section. By restricting outside access to the data members in a class, it is easier to ensure the integrity and consistency of their values.

- 158. Members of the **private** section of a class are intended to be used only by the members of that class.

- 159. An & in the return type for a function or operator indicates that a reference return is being performed. In a reference return, a reference to the actual object in the return expression rather than a copy is returned. The scope of the returned object should not be local to the invoked function or operator.

- 160. When creating a **friend** function, use the keyword friend in the prototype in the class definition, but do not use this keyword in the actual function definition. Friend functions are defined outside the class definition.

- 161. Friend functions have access to the private and protected members of a class.

- 162. An operator can be overloaded many times using distinct signatures.

- 163. If we want to overload a binary operator with two different types of operands with a non-class as the first operand, we must use a **friend** function to define the operator overloading.

- 164. Do not use implicit type conversions unless it is necessary. If they are used arbitrarily, it can cause problems for future users of the class.

- 165. Whenever we use **new** in a constructor to allocate memory, we should use **delete** in the corresponding destructor to free that memory.

- 166. The relationship “is-a” indicates inheritance. For example, a car is a kind of vehicle.

- 167. The relationship “has-a” indicates containment. For example, a car has an engine. Aggregate objects are constructed using containment.

- 168. Both inheritance and containment facilitate software reuse.

- 169. A new class that is created from an existing class using the principle of inheritance is called a _derived class_ or _subclass_. The parent class is called the _base class_ or _superclass_.

- 170. When an object that is an instance of a derived class is instantiated, the constructor for the base class is invoked before the body of the constructor for the derived class is invoked.

- 171. A class intended to be a base class usually should use **protected** instead of **private** members.

- 172. When a derived class object is being created, first, its base classes’ constructors are called before its own constructor. The destructors are called in the reverse order.

- 173. A constructor of a derived class must pass the arguments required by its base class constructor.

- 174. A derived class uses the member functions of the base class unless the derived class provides a replacement function with the same name.

- 175. A derived class object is converted to a base class object when used as an argument to a base class member function.

- 176. Derived class constructors are responsible for initializing any data members added to those inherited from the base class.
