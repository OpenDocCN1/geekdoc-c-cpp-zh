# 9.15 `static` Class Members

There is an important exception to the rule that each object of a class has its own copy of all the data members of the class. In certain cases, *only one* copy of a variable should be *shared by all* objects of a class. A **static** data member is used for these and other reasons.

Such a variable represents “classwide” information, i.e., data that is shared by *all* instances and is *not* specific to any one object of the class. Recall, for example, that the `GradeBook` classes in **Chapter 7** use `static` data members to store constants representing the number of grades that all `GradeBook` objects can hold.