However, if required, we can create custom exception classes either locally in the program or globally in Class Builder. We’ll look at how to implement both options next.

# 9.3.3 Defining Exception Classes Globally

Most often, we define exception classes globally so that they can be used in multiple programs. The steps to create an exception class in Class Builder are similar to those to create any regular class, except that the exception class must inherit `CX_STATIC_CHECK`, `CX_DYNAMIC_CHECK`, or `CX_NO_CHECK`, or any class that inherits these classes.

In addition, exception classes should follow the naming convention of `CX_` for the SAP namespace and `ZCX_` for customer namespace. The EXCEPTION CLASS checkbox is also checked for the exception class.

Follow these steps to define an exception class in Class Builder:

+   1. Enter the name of the exception class on the Class Builder initial screen (Transaction SE24) and click the CREATE button. The name of the exception class should start with `ZCX_`, as shown in Figure 9.14.

![](bbox=[0.148, 0.524, 0.626, 0.689])

**Figure 9.14** Class Builder: Initial Screen

+   2. The system will present the properties dialog box. Because you used the naming convention `ZCX_`, the system automatically assigns `CX_STATIC_CHECK` under SUPERCLASS and selects the EXCEPTION CLASS radio button under CLASS TYPE, as shown in Figure 9.15. Optionally, you can change the superclass to `CX_DYNAMIC_CHECK` or `CX_NO_CHECK` or any class that inherits these abstract classes. Maintain a description for the class and set the preferred instantiability for the class, as shown in Figure 9.15.