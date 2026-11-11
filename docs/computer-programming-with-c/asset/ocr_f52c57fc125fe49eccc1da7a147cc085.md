![](bbox=[0.189, 0.109, 0.84, 0.504])

**Figure 14.1:** Principle of inheritance

+   3. Gender
+   4. Roll Number(roll_no)
+   5. Marks

Also, for every Professor object, we plan to store following information in computer memory:

+   1. Name
+   2. Date of Birth
+   3. Gender
+   4. Professor Identifier(prof_id)
+   5. Salary

Figure 14.2 shows the attributes of classes Student and Professor with the attribute differences highlighted in boldface.

Having members name, dob, and gender is a common requirement of Student and Professor classes. Instead of duplicating this code in both the classes, we can create a common parent class named as Person which defines the common members. We then create Student and Professor as child classes of class Person as shown in the Figure 14.3. As we have created a relationship of inheritance, all the child classes will