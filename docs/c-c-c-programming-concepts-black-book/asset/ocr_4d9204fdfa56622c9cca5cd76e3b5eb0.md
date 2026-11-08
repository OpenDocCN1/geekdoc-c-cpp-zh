# Collaboration

Collaboration is a society of classes, interfaces, and other elements that work together to provide some cooperative behavior that is larger than the sum of its parts.

# Relationships

To explain relationships, we need to go back again to our discussion on UML. We would use UML as a reference to explain relationships. We can draw an UML using the following kinds of relationships:

+   - **Include**—If any process needs the outcome of another process, then the relationship existing between them is called “Include” relationships. For example, for borrowing a CD from a CD store, you need to verify whether that CD actually exists in the shop. Thus, borrowing a CD includes the verification process. Also, in ATM, to withdraw money, the machine needs to verify the card identity. Thus, withdrawing money from the ATM includes card verification process. Figure 23.12 shows the diagrammatical representation of an include relationship:

![](bbox=[0.271, 0.363, 0.729, 0.423])

**Figure 23.12:** Illustrating the Include Relationship

+   - **Extend**—Depending on the condition, if any process needs to have a sub-process, we can relate them using the Extend relationship. For example, to avail discount on a flight ticket, one can have two sub-processes for domestic flight and international flight, and they are bound with their parent process using an extend relationship. Here, the condition we can define is of flight type. Figure 23.13 specifies the notation used to describe an extend relationship:

![](bbox=[0.268, 0.516, 0.756, 0.7])

**Figure 23.13:** Illustrating an Extend Relationship

+   - **Generalization**—Generalization has one parent process and one or more child processes, where each child process describes a specialized type of its parent process. For example, in a store, we can make payment through cash or card. Thus, payment by cash and payment by card are two child processes of the process payment. Figure 23.14 describes one generalization relationship: