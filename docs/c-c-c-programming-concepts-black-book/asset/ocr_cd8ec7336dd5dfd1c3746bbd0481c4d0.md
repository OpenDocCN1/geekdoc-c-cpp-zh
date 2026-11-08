# Chapter 23

# Behavioral Diagrams

Behavioral diagrams visualize, specify, construct, and document the dynamic aspects of a system. In these diagrams, we basically emphasize on the interaction between objects and the flow of control among them. This flow of control may be simple or complex and may involve branching, looping, recursion, and concurrency. There are four types of behavioural diagrams, which are discussed in the following subsections.

# Use-Case Diagram

A use-case diagram shows a set of use cases, actors, and their relationships. It is used to model the requirement of a system. It comprises use cases, actors, dependency, generalization, association, relationship, roles, subsystems, and classes. Figure 23.23 shows a use-case diagram:

![](bbox=[0.264, 0.32, 0.749, 0.5])

**Figure 23.23:** Relationship among Use Cases

# Interaction Diagram

Interaction diagrams describe the flow of messages between objects.

# Sequence Diagram

Sequence diagram is a type of interaction diagram that focuses on the order in which the messages are sent. It is very useful for describing the procedural flow through many objects and for finding race conditions in concurrent systems. In UML, it is shown as a table that shows objects arranged along the X-axis and messages ordered in increasing time along the Y-axis.

To go into depth of sequence diagrams, we give a brief introduction of the *Model-View-Controller* (MVC) architecture.

# MVC Architecture

The MVC pattern separates the modeling of the domain, the presentation, and the actions based on user input into three separate set of classes, which are as follows:

+   - **Model**—This manages your behavior and data in the application domain, responds to requests for specifics of its state (usually through the view), and responds to instructions to switch state (usually through the controller).
+   - **View**—The view manages the display of information.
+   - **Controller**—The controller interprets inputs from the user, informing the model and/or the view to change as appropriate.