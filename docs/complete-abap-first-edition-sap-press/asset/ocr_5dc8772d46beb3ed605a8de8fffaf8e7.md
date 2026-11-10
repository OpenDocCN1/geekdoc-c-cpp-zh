```
ENDCLASS.
CLASS cl_parent IMPLEMENTATION.
  METHOD set_value.
  ENDMETHOD.
  METHOD check_value.
  ENDMETHOD.
  METHOD reset_value.
  ENDMETHOD.
ENDCLASS.
CLASS cl_child DEFINITION INHERITING FROM cl_parent.
ENDCLASS.
CLASS cl_child IMPLEMENTATION.
ENDCLASS.
DATA child TYPE REF TO cl_child.
START-OF-SELECTION.
  CREATE OBJECT child.
  child->set_value( value = 'child' ).
```

# Listing 8.18 Inheritance Example

In Listing 8.18, the `cl_child` class is defined as a subclass of `cl_parent`. Here, `cl_parent` is the superclass, and it implements the `set_value` method in the public section, the `check_value` method and the `value` attribute in the protected section, and the `reset_value` method in the private section.

The `cl_child` class is inherited from `cl_parent` using the inheriting from addition of the class definition statement. This sets the parent-child relationship between the two classes. The `cl_child` class doesn't list any components on its own. All the components in the public and protected sections of the `cl_parent` superclass are, by default, available to the `cl_child` subclass. This is shown in the program code under `start-of-selection` (see Listing 8.18), where a reference object child is defined by referring to `cl_child` and the `set_value` method of `cl_parent` is accessed using this child class reference with the statement `child->set_value( value = 'child' ).`

Keep the following important points about inheritance in mind:

+   - The subclass can access the components defined under public and protected visibility sections in the superclass.
+   - You can't define a component in a subclass with the same name as the component in the public or protected sections of the superclass.
+   - Because the private section of the superclass is invisible to the subclass, you can define a component in the subclass with the same name as the component in the superclass.