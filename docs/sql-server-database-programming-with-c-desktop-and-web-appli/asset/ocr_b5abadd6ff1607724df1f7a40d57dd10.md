# Data Updating and Deleting with Visual #NET

| faculty_id | faculty_name | title | office | phone | college | email | fimage |
|---|---|---|---|---|---|---|---|n| B78880 | Ying Bai | Associate Professor | MTC-211 | 750-378 | Florida Atlantic University | ybai@college.net | NULL |

**Figure 7.13** The data to be recovered in the faculty table.

| course_id | course | credit | classroom | enrollment | faculty_id |
|---|---|---|---|---|---||
| CSC-132B | Introduction to Programming | 3 | MTC-302 | T-H: 1:00-2:25 PM | 21 | B78880 |
| CSC-234A | Data Structures & Algorithms | 5 | MTC-302 | M-W: 9:00-9:55 AM | 25 | B78880 |
| CSE-434 | Advanced Electronics | 3 | MTC-213 | M-W: 9:00-1:55 PM | 26 | B78880 |
| CSE-438 | Advd Logic & Microprocessor | 3 | MTC-213 | M-W: 11:00-11:55 AM | 35 | B78880 |

**Figure 7.14** The data to be recovered in the course table.

| user_name | pass_word | faculty_id | student_id |
|---|---|---|--|
| ybai | come | B78880 | NULL |

**Figure 7.15** The data to be recovered in the login table.

| course_id | student_id | course_id | credit | major |
|---|---|---|---|--|
| 1005 | A778896 | CSC-234A | | CS/IS |
| 1009 | A788335 | CSE-434 | | 3 CE |
| 1014 | A788335 | CSE-438 | | 3 CE |
| 1016 | A978850 | CSC-132B | | 3 ISE |
| 1017 | A978850 | CSC-234A | | 3 ISE |

**Figure 7.16** The table order be recovered in Figure 7.12 and refer to Figures 7.13–7.16 to complete these records recovery.

A complete project **SelectWizard Project** can be found from a folder DB Projects\ Chapter 7\ SelectWizard Wizards are located in the **Students** folder of the CRC press site (refer to Figure 1.2 in Chapter 1).

# PART II UPDATING AND DELETING WITH RUNTIME OBJECTS

To update or delete the database using the runtime object method is a flexible and professional way to perform data modifications in the Visual #NET environment. Compared with the method we discussed in Part I, in Visual Studio.NET Design Tools and Wizards are utilized to update or delete data database, the runtime object method provides more sophisticated techniques to do this efficiently and conveniently a more complicated job being needed. Relatively speaking, the method we discussed in the first part is easy to learn and code, but the method has some limitations. First, each TableAdapter built by the TableQuery Configuration Wizard can only perform a single query as data updating or deletion. After, the query function is built, no modifications can be made to that functionally, which means that the only times that you can modify query function are after the project runs or after the project terminates. In other words, you cannot modify query function during the project runs.

To overcome these shortcomings, we will discuss how to update or delete data using the runtime object method in this part.