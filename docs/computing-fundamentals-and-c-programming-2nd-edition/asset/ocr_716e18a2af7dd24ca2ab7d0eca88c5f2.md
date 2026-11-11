# ## CHAPTER 9

# # Array

# ### LEARNING OBJECTIVES

After reading this chapter, you will be able to

+   - **LO 9.1** Define the concept of arrays
+   - **LO 9.2** Determine how one-dimensional array is declared and initialized
+   - **LO 9.3** Understand the concept of two-dimensional arrays
+   - **LO 9.4** Discuss how two-dimensional array is declared and initialized
+   - **LO 9.5** Describe multi-dimensional arrays
+   - **LO 9.6** Explain dynamic arrays

# ## 9.1 INTRODUCTION

So far we have used only the fundamental data types, namely **char**, **int**, **float**, **double** and variations of **int** and **double**. Although these types are very useful, they are constrained by the fact that a variable of these types can store only one value at any given time. Therefore, they can be used only to handle limited amounts of data. In many applications, however, we need to handle a large volume of data in terms of reading, processing and printing. To process such large amounts of data, we need a powerful data type that would facilitate efficient storing, accessing and manipulation of data items. C supports a derived data type known as *array* that can be used for such applications.

An array is a *fixed-size* sequenced collection of elements of the same data type. It is simply a grouping of like-type data. In its simplest form, an array can be used to represent a list of numbers, or a list of names. Some examples where the concept of an array can be used:

+   - List of temperatures recorded every hour in a day, or a month, or a year.
+   - List of employees in an organization.
+   - List of products and their cost sold by a store.
+   - Test scores of a class of students.