# 13.1 Introduction

In Chapter 12, we developed an object-oriented design for our ATM system. We now implement our object-oriented design in Java. In Section 13.2, we show how to convert class diagrams to Java code. In Section 13.3, we tune the design with inheritance and polymorphism. Then we present a full Java code implementation of the ATM software in Section 13.4. The code is carefully commented and the discussions of the implementation are thorough and precise. Studying this application provides the opportunity for you to see a more substantial application of the kind you’re likely to encounter in industry.

# 13.2 Starting to Program the Classes of the ATM System

[Note: This section can be taught after Chapter 8.]

# Visibility

We now apply access modifiers to the members of our classes. We’ve introduced access modifiers public and private. Access modifiers determine the visibility or accessibility of an object’s attributes and methods to other objects. Before we can begin implementing our design, we must consider which attributes and methods of our classes should be public and which should be private.

We’ve observed that attributes normally should be private and that methods invoked by clients of a given class should be public. Methods that are called as “utility methods” only by other methods of the same class normally should be private. The UML employs visibility markers for modeling the visibility of attributes and operations. Public visibility is indicated by placing a plus sign (+) before an operation or an attribute, whereas a minus sign (–) indicates private visibility. Figure 13.1 shows our updated class diagram with visibility markers included. [Note: We do not include any operation parameters in Fig. 13.1—this is perfectly normal. Adding visibility markers does not affect the parameters already modeled in the class diagrams of Figs. 12.17–12.21.]

# Navigability

Before we begin implementing our design in Java, we introduce an additional UML notation. The class diagram in Fig. 13.2 further refines the relationships among classes in the ATM system by adding navigability arrows to the association lines. Navigability arrows (represented as arrows with stick (→) arrowheads in the class diagram) indicate in the