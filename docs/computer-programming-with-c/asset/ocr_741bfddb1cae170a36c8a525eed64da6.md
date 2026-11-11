+   3. Courses offered by the institute
+   4. Departments of the institute, etc.

So as to store the data about these real world entities, we can create different classes in the C++ program such that each of the class combines the ‘data’ and ‘functions’ required to manage the information about one entity in the real world as shown in Figure 1.15. Hence, we can create classes named as Student, Professor, Course and Department so as to store representing each of the respective real world entities.

![](bbox=[0.256, 0.241, 0.628, 0.528])

Figure 1.15: Example of classes in C++

Note that, each class combines related ‘data’ and ‘functions’ together. For example, the class Student contains the data elements named as roll_no, name and marks which indicates that for every student in the institute we will be storing the roll number, name and marks of the student object in computer memory. Further, the functions defined in class Student represent the operations that a student object can perform in the real world. The function save_student() indicates that the student object can save his/her details online by registering on the website of the institute. The presence of the function give_exam() in the class Student indicates that the student in the real world can appear for an online exam which is deployed on the web site of the educational institute and the function print_result() indicates that student can take a printout of his/her result, which prints the marks obtained by the student in the online examination. Similarly, we can imagine the meaning of data and functions which we have shown in other classes as shown in Figure 1.15.

The object-oriented program organizes the code based on the ‘data’ and hence it makes the large programs easy to maintain and support. The details of object-oriented programming paradigm along with its features are discussed in Chapters 11 to 14 of this text book. The key features of the object-oriented programming paradigm are as listed below. We have just given one liners for each of these features, however, understanding