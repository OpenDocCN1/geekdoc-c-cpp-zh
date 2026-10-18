important issue is to decide what functions are to be provided. For a class to be useful, it must contain the following functions, in addition to the service functions:

+   1. Class management functions.
+      - How an object is created?
+      - How an object is destroyed?
+   2. Class implementation functions.
+      What operations are performed on the data type of the class?
+   3. Class access functions.
+      How do we get information about the internal variables of the class?
+   4. Class utility functions.
+      How do we handle errors?

Other issues that are to be considered are:

+   1. What kind of access controls are required for the base classes?
+   2. Which functions can be made virtual?
+   3. What library classes are expected to be used in a class?
+   4. The design of the individual classes has a major impact on the overall quality of the software.

Given below are some guidelines which should be considered while designing a class:

+   1. The public interface of a class should have only functions of the class.
+   2. An object of one class should not send a message directly to a member of another class.
+   3. A function should be declared public only when it is required to be used by the objects of the class.
+   4. Each function either accesses or modifies some data of the class it represents.
+   5. A class should be dependent on as few (other) classes as possible.