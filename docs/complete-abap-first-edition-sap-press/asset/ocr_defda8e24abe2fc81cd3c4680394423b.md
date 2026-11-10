In Listing 8.28, three classes are defined: `cl_parent`, `cl_child1`, and `cl_child2`. `cl_child1` inherits from `cl_parent`, and `cl_child2` inherits from `cl_child1`.

A narrow cast is first performed by assigning the `child2` object to the parent object, and then a widening cast is performed by assigning the `parent` object to `child1`. When the `meth2` method is called using the `child1` object reference after the widening cast, it will execute the code in the `meth2` method of the `cl_child2` class.

# 8.4.3 Dynamic Binding with the CALL Method

When an object is passed to the method as a parameter, the system automatically binds the object dynamically. This allows us to design objects that are easily extendable.

To understand dynamic binding with the `CALL` method, let's look at the code snippet in Listing 8.29. Here, we've defined `cl_student` as an abstract class with `tuition_fee` and `get_fee` as abstract methods with public visibility. A `fee_paid` attribute that can be set if the fee is paid by the student is defined in the protected section.

Two classes, `cl_commerce_student` and `cl_science_student`, inherit the `cl_student` class and maintain their own implementation of the `tuition_fee` and `get_fee` abstract methods. In the `tuition_fee` method, the private `fee_paid` attribute is set to `abap_true` if the student has paid the fee. The `get_fee` method returns the value of the private `fee_paid` attribute.

We've defined one `cl_admission` class that can be used to enroll a student in a course. This class has two methods, `set_student` and `enroll`, which can be used to complete the admission of the student in a course. Because this `cl_admission` class should be able to enroll any student from any student category (science student, commerce student, etc.), we need to design this class to import information about any student category.

The `set_student` method of the `cl_admission` class is defined with an importing parameter to import the `student` object. If we maintain the static type of this importing parameter as `cl_commerce_student`, it can only import the commerce student object and our class can only process the admission for commerce students. Similarly, if we maintain the static type of the importing parameter as `cl_science_student`, it can only import the science student object and our class can