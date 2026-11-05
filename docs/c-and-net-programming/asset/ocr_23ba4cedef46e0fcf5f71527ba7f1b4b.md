5. When a method is declared as a virtual method in a base class then that method can be defined in a base class and it is optional for the derived class to override that method. The overriding method also provides more than one form for a method. Hence it is a polymorphism.

6. When a method is declared as a virtual method in a base class and that method has the same definition in a derived class then there is no need to override it in the derived class. But when a virtual method has a different definition in the base class and the derived class then there is a need to override it in the derived class.

7. When a virtual method is invoked, the **run-time type of** the object is checked for an overriding member. The overriding member in the derived class is called, which might be the original member, if no derived class has overridden the member.

8. One can add derived types without modifying the rest of the program. The runtime type of objects thus determines behavior.

9. The virtual modifier tells the compiler that when any class is derived from other class an override method should be called, upon its invocation.

10. By default, methods are non-virtual. One can't override a non-virtual method.

4. One can't use the virtual modifier with the static, abstract, private or override modifiers.

5. The virtual keyword is used to modify a method, property, indexer, or event declared in the base class and allows it to be overridden in the derived class.

6. The override keyword is used to extend or modify a virtual/abstract method, property, indexer, or event of base class into derived class.

# 7. Difference between virtual and non-virtual methods.

When virtual and non-virtual methods are called by class's instance then according to the run type the instance virtual method implementation is invoked; in other words in case of virtual method class's instances invoke the subclass override method and the non-virtual method invoked is determined based on the instance of the class.

# 8. Calling virtual method of the base class from derived class which is overridden in derived class – .

The base class method implementation can be called from derived class method by using member access operator (.) and the name of the base class.