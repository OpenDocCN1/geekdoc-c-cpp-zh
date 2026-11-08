
Figure 23.3 shows a class with attributes and operations:

![](img/43c5f409f9b17790a628c4b4df854b61_793_0.png)

**Figure 23.3: Showing Class with Attributes and Operations**

## Object-Oriented Analysis

The object model has influenced even earlier phases of the software development life cycle. The conventional structured analysis emphasizes the flow of data within a system, whereas Object-Oriented Analysis (OOA) focuses on real-world models using object-oriented view of the real world. Grady Booch defined OOA as:

> *Object-oriented analysis is a method of analysis that examines requirements from the perspective of the classes and objects found in the vocabulary of the problem domain.*

Precisely, how are OOA, OOD, along with OOP related? Essentially, the products associated with OOA function as models from which we might start an object-oriented style; the products associated with object-oriented design may then be used like blueprints for completely implementing something using object-oriented encoding methods.

In an object-oriented approach, in the analysis phase, the emphasis is on discovering and describing objects in the problem domain.

In OOA, we focus on doing the right thing. OOA includes:

- **Use Case Model** – It captures the functionality the system should provide from the user’s perspective. It does not specify how the system actually implements the system. In essence, it helps to systematically identify the system’s responsibilities from the user requirements perspective.
- **Use Cases** – It includes stories or scenarios of how people use the system.
- **Use Case Diagram** – It gives a high-level view of how different users interact with the system through use cases.

Thus, Use Case Model = Use Cases + Use Case Diagrams.

In OOA, we have two types of model to define any scenario: one is Use Case Model and the other is Domain Model. The use case model consists of use case templates and use case diagram. We can define use cases of a scenario as the goals set for the system to achieve and/or it must produce. It mainly describes the interaction between the user and the system. Textual descriptions used in use cases generally express several scenarios. In a single sentence, we can define use case as a set of goals performed by the system, which is of value for one or more actors and other stakeholders of the system. The use case model, on the other hand, can be defined as below:

- Use Case Model captures the functionality of the system that should be provided from the user’s perspective.
- It does not specify how the system actually implements the system.
- In essence, it helps to identify responsibility of the system in user requirement perspective.

In the use case model, users are defined either as an actor or as a stakeholder, where actors of the system are bound to achieve some goals, whereas the stakeholders do not always need to achieve any goals. We will mainly deal with actors while documenting or diagrammatically representing use case model.

Again, the goals of the system are defined as "In Scope Goal" and "Out Scope Goal." In scope goals are the use cases, and the out scope goal represents the relationship between actor and the use case. In scope goals are again divided into two types:

- **Sea-Level Goal**—Sea-level goals are directly accessible to the actor. Thus, the main use cases represent sea-level goals.
- **Fish-Level Goal**—In case of business validation, actor does not have access to these use cases. These are called fish-level goals.

### Classifier

A classifier is a mechanism that describes structural and behavioral features of classes and objects. In UML, the important classifiers are class, interface, data types, signals, components, nodes, use case, and subsystems.

### Requirements Analysis

1. Identify the users and their goals. Figure 23.4 shows the users:

   ![](img/43c5f409f9b17790a628c4b4df854b61_794_0.png)

2. Develop use cases model (use cases and use case diagram). Figure 23.5 shows the use case diagram:

   ![](img/43c5f409f9b17790a628c4b4df854b61_794_1.png)

3. Develop domain model (conceptual class diagram).

Before explaining the use-case diagram and conceptual class diagram with an example, we first explain how a use case template looks like.

### Use Case Template

Use case template represents the documented scenario of a use case diagram. It has a common set of points that defines various attributes of a use case. In the following paragraph, a template has been given that can be used to produce any project-specific use case documentation. For each use case used in a use case diagram, we need to write a separate use case template with the following points:

- Overview
- Actors
- Stakeholders
- Pre and Post Conditions
- Normal Flow
- Alternate Flow(s)
- Exceptions
- Extend

## 水利水电工程勘测设计专业技术人员继续教育大纲

### 第一部分 水利水电工程勘测设计专业技术人员继续教育大纲

第一条 为加强水利水电工程勘测设计专业技术人员继续教育工作，提高专业技术人员素质，根据《专业技术人员继续教育规定》(人社部令第25号)、《水利专业技术人员继续教育管理办法(试行)》等有关规定，制定本大纲。

第二条 本大纲适用于水利水电工程勘测设计专业技术人员继续教育。

第三条 水利水电工程勘测设计专业技术人员继续教育内容分为专业科目和公需科目。

第四条 专业科目包括水利水电工程勘测设计相关的法律法规、政策文件和标准规范，水利水电工程勘测设计专业理论知识、技术方法及实践能力训练等。

第五条 公需科目包括专业技术人员应当普遍掌握的政治理论、法律法规、职业道德、信息技术、国情水情等基本知识。

第六条 专业科目学时数一般不少于当年总学时的三分之二。

- **Flexibility in Information Representations**—An object might admit a number of different data representations, which could change within the interest of efficiency as the program is running. The item notion provides a uniform way of providing access to this kind of changing objects.

If, however, the client was permitted immediate access to the attributes of the object without using techniques, the representation could in no way be changed without invalidating the actual code that accessed the individuals' attributes.

The simplest kind of method for setting the worthiness of an attribute is known as a setter, while the easiest type for getting the worthiness of an attribute is known as a getter. For instance, if we had some type of shape class with fill up represented by an int, we'd expect the following to see inside our class declaration method headers:

```
setFill(int Fill)
int getFill()
```

### Operation

An operation is the implementation of a service that can be requested from any object of the class to affect the behavior of the class. In UML, they are listed in the compartment just below the class attribute, as shown in Figure 23.6.

![](img/43c5f409f9b17790a628c4b4df854b61_796_0.png)

### Interface

An interface is a collection of operations that are used to specify a service of a class or a component. Figure 23.7 shows an interface:

![](img/43c5f409f9b17790a628c4b4df854b61_796_1.png)

### Signal

A signal is the specification of an asynchronous stimulus communicated between instances.

### Component

A component is a physical and replaceable part of a system that conforms to and provides the realization of a set of interfaces. In UML, it is shown as a rectangle with tabs, as shown in Figure 23.8:

![](img/43c5f409f9b17790a628c4b4df854b61_797_0.png)

### Node

A node is a physical element that exists at runtime and represents a computational resource generally having a large memory and often process capability. The UML notation is shown in Figure 23.9:

![](img/43c5f409f9b17790a628c4b4df854b61_797_1.png)

### Package

A package is a general-purpose mechanism for organizing elements into groups. It can also contain other packages. Packages are widely used in a Java-based environment. The UML notation is shown in Figure 23.10:

![](img/43c5f409f9b17790a628c4b4df854b61_797_2.png)

### Subsystem

A subsystem is a group of elements of which some contribute a specification of the behavior offered by other contained elements.

### Object

An object is an instance of a class. The object could be shown as the instance of a class with the path name along with the attributes. Multiple objects are connected through links. Figure 23.11 shows some basic notation of objects that are used in UML:

![](img/43c5f409f9b17790a628c4b4df854b61_797_3.png)
