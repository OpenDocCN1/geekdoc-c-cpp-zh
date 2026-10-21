![](bbox=[0.05, 0.12, 0.68, 0.38])

# Fig. 1.3 Inter-relationship between programs and entities

marksheet printing, the third is maintaining the subject (i.e., provide adding, deleting, and modifying details of a subject), and the fourth is maintaining the teacher's information (i.e., providing adding, deleting, and modifying details of a teacher). There are five entities considered—roll call, teacher, student, marksheet, and subject. Again, there are possibly many more, but they have not been considered for simplicity. Figure 1.3 shows the association of each entity with each program. The actual system design process might generate a large number of programs and a larger number of entities in more than one way. The following example will illustrate the concept.

![](bbox=[0.07, 0.42, 0.48, 0.62])

# Fig. 1.4 Determining relations among entities

Once we decide the data and function attributes of the program, the next step is to find the relation between the different entities by asking a few simple questions.

‘How is a teacher associated with the roll call?’ is one such question. One answer may associate a teacher with the roll call as the person who takes it for his/her subject. We may need to obtain the information about the corresponding teacher from the roll call entity. Figure 1.4 shows an example of a message being asked and replies being sought from an entity. The question or the query is normally referred to as a request and the reply is termed as the response.

> When a program uses objects to represent real-world entities, its end users ask queries to the objects and seek responses by passing and receiving messages.

When we look at our job to be done, we need to have few more such cases of requests and responses, for example, a teacher asking how many students were present on a particular day in the class and the roll call entity answering that question. We may need to find out how many such questions are possible to be asked and how the answers to these questions are sought out. This is the next assignment when we are developing our system. The method to generate the answer of a message must be provided to the receiving entity; otherwise, the receiving entity cannot answer that question. In the case of the question regarding the number of students present, the roll call entity must have a method to calculate the total students present from the data it has. This method is called or invoked by the receiving entity when the other entity asks for that specific information.

# 1.3 CLASSES AND OBJECTS

A class is an extension to the C struct (the basic C struct is also extended in C++; we will examine the difference later). Let us consider an example of a class Student. The struct Student in C will contain only the attributes of the student such as name and address. On the other hand, in C++, the class Student will have the attributes of the student and it will also store the actions (or functions) related to the student. This means that the student class will contain the student name, address, roll number, subjects, etc., as well as all actions in