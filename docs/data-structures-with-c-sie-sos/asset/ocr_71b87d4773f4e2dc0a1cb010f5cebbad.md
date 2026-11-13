Remark: Suppose a file is sorted numerically by social security number. As new records are inserted into the file, data must be constantly moved to new locations in order to maintain the sorted order. One simple way to minimize the movement of data is to have the social security number serve as the address of each record. Not only would there be no movement of data when records are inserted, but there would be instant access to any record. However, this method of storing data would require one billion (10^9) memory locations for only hundreds or possibly thousands of records. Clearly, this tradeoff of space for time is not worth the expense. An alternative method is to define a function H from the set K of key values—social security numbers—into the set L of addresses of memory cells. Such a function H is called a *hashing function*. Hashing functions and their properties will be covered in Chapter 9.

# SOLVED PROBLEMS

# Basic Terminology

+   1.1 A professor keeps a class list containing the following data for each student:
+   Name, Major, Student Number, Test Scores, Final Grade
+   (a) State the entities, attributes and entity set of the list.
+   (b) Describe the field values, records and file.
+   (c) Which attributes can serve as primary keys for the list?

+   (a) Each student is an entity, and the collection of students is the entity set. The properties, name, major, and so on, of the students are the attributes.
+   (b) The field values are the values assigned to the attributes, i.e., the actual names, test scores, and so on. The field values for each student constitute a record, and the collection of all the student records is the file.
+   (c) Either Name or Student Number can serve as a primary key, since each uniquely determines the student's record. Normally the professor uses Name as the primary key, but the registrar may use Student Number.

+   1.2 A hospital maintains a patient file in which each record contains the following data:
+   Name, Admission Date, Social Security Number, Room, Bed Number, Doctor
+   (a) Which items can serve as primary keys?
+   (b) Which pair of items can serve as a primary key?
+   (c) Which items can be group items?

+   (a) Name and Social Security Number can serve as primary keys. (We assume that no two patients have the same name.)
+   (b) Room and Bed Number in combination also uniquely determine a given patient.
+   (c) Name, Admission Date and Doctor may be group items.

+   1.3 Which of the following data items may lead to variable-length records when included as items in the record: (a) age, (b) sex, (c) name of spouse, (d) names of children, (e) education. (f) previous employers?