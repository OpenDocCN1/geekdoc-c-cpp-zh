![](bbox=[0.13, 0.14, 0.21, 0.22])

The words *static* and *dynamic* come up again and again in the computer world. *Static* refers to something fixed and unchangeable, while *dynamic* refers to something that changes:

+   - In your application, a class is static because you describe it in your code; and after you have described your class, it does not change while the application is running. A class has a certain set of member variables and member functions that you specify in the code. Although the application is running, the members of a class do not change.
+   - The objects, however, are considered to be dynamic, because they can come to life while the application is running; their member variables can change, and they can be deleted.

**Table 2-1 Static Diagrams of UML**

| Diagram Type | What It Shows |
|---|---|
| Class diagram | The different classes |
| Component diagram | The different parts of the system; each part contains classes related to each other |
| Deployment diagram | The different computers and hardware involved |

The following list describes the items in Table 2-1 in a bit more detail:

+   - **Class diagram:** The class diagram shows the different classes and their relationships to each other. For example, a class diagram might show that the class called *Skiddle* is derived from the class *Skaddle*, and it might show that the class *Skaddle* contains as a member a list of *Ruddle* instances. Typically as you work on a class diagram, you will also be adding and modifying the classes from the model itself.
+   - **Component diagram:** The component diagram shows the major parts of your software system. For example, all the parts dealing with *Discombobulation*, including the *Discombobulator* class and the *Perturburator* class as well as other related classes, might all be grouped into a single component called *SuperSystem*.
+   - **Deployment diagram:** The deployment diagram shows a hardware view of your system. This might include specific computers (such as a *Compaq Presario* with a gigabyte of RAM), or it might include more abstract hardware components, such as *Internet connection*. Or it might show hardware components even more generic, such as *network node* or *database server*. Nevertheless, these are all hardware components.