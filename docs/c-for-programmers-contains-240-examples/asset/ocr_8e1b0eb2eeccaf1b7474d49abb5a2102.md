# Software Engineering Observation 3.6

> Member functions that set the values of private data should verify that the intended new values are proper; if they are not, the set functions should place the private data members into an appropriate state.

A class’s set functions can return values to the class’s clients indicating that attempts were made to assign invalid data to objects of the class. A client of the class can test the return value of a set function to determine whether the client’s attempt to modify the object was successful and to take appropriate action. In Chapter 16, we demonstrate how clients of a class can be notified via the exception-handling mechanism when an attempt is made to modify an object with an inappropriate value. To keep the program of Figs. 3.15–3.17 simple at this early point in the book, setCourseName in Fig. 3.16 just prints an appropriate message on the screen.

# 3.11 (Optional) Software Engineering Case Study: Identifying the Classes in the ATM Requirements Specification

Now we begin designing the ATM system that we introduced in Chapter 2. In this section, we identify the classes that are needed to build the ATM system by analyzing the nouns and noun phrases that appear in the requirements specification. We introduce UML class diagrams to model the relationships between these classes. This is an important first step in defining the structure of our system.

# Identifying the Classes in a System

We begin our OOD process by identifying the classes required to build the ATM system. We’ll eventually describe these classes using UML class diagrams and implement these classes in C++. First, we review the requirements specification of Section 2.7 and find key nouns and noun phrases to help us identify classes that comprise the ATM system. We may decide that some of these nouns and noun phrases are attributes of other classes in the system. We may also conclude that some of the nouns do not correspond to parts of the system and thus should not be modeled at all. Additional classes may become apparent to us as we proceed through the design process.

Figure 3.18 lists the nouns and noun phrases in the requirements specification. We list them from left to right in the order in which they appear in the requirements specification. We list only the singular form of each noun or noun phrase.

We create classes only for the nouns and noun phrases that have significance in the ATM system. We do not need to model “bank” as a class, because the bank is not a part of the ATM system—the bank simply wants us to build the ATM. “Customer” and “user” also represent entities outside of the system—they are important because they interact with our ATM system, but we do not need to model them as classes in the ATM software. Recall that we modeled an ATM user (i.e., a bank customer) as the actor in the use case diagram of Fig. 2.14.

We do not model “$20 bill” or “deposit envelope” as classes. These are physical objects in the real world, but they are not part of what is being automated. We can adequately represent the presence of bills in the system using an attribute of the class that models the cash dispenser. (We assign attributes to classes in Section 4.11.) For example, the cash dispenser