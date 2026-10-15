![](bbox=[0.38, 0.14, 0.72, 0.27])

# FIGURE 9.2 A UML class diagram showing multiple inheritance

child class to have multiple parents. This approach is called multiple inheritance and is occasionally useful for describing objects that are in between two categories or classes. For example, suppose we had a class Car and a class Truck and we wanted to create a new class called PickupTruck. A pickup truck is somewhat like a car and somewhat like a truck. With single inheritance, we must decide whether it is better to derive the new class from Car or Truck. With multiple inheritance, it can be derived from both, as shown in Figure 9.2.

Multiple inheritance works well in some situations, but it comes with a price. What if both Truck and Car have methods with the same name? Which method would PickupTruck inherit? The answer to this question is complex, and it depends on the rules of the language that supports multiple inheritance.

The designers of the Java language explicitly decided not to support multiple inheritance. Instead, we can rely on interfaces to provide the best features of multiple inheritance without the added complexity. Although a Java class can be derived from only one parent class, it can implement multiple interfaces. Therefore, we can interact with a particular class in specific ways while inheriting the core information from one parent class.

# SELF-REVIEW QUESTIONS (see answers in Appendix N)

+   SR 9.1 Describe the relationship between a parent class and a child class.
+   SR 9.2 How does inheritance support software reuse?
+   SR 9.3 What relationship should every class derivation represent?
+   SR 9.4 What does the protected modifier accomplish?
+   SR 9.5 Why is the super reference important to a child class?
+   SR 9.6 Define a class SchoolBook2 that extends Book2 to include an attribute indicating the age (4 through 16) that a book targets. The constructor accepts the age as a parameter. The class also provides a level