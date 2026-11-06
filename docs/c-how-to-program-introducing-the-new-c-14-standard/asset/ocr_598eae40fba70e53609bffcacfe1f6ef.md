# 7.1 Introduction

This chapter introduces the topic of **data structures**—*collections* of related data items. We discuss `arrays`, which are *fixed-size* collections consisting of data items of the *same type*, and `vectors`, which are collections (also of data items of the *same type*) that can grow and shrink *dynamically* at execution time. Both `array` and `vector` are C++ standard library class *templates*. To use them, you must include the `<array>` and `<vector>` headers, respectively.

After discussing how `arrays` are declared, created and initialized, we present examples that demonstrate several common `array` manipulations. We show how to *search* `arrays` to find particular elements and *sort* `arrays` to put their data in *order*.

We build two versions of an instructor `GradeBook` case study that use arrays to maintain sets of student grades *in memory* and analyze student grades. We introduce the *exception-handling* mechanism and use it to allow a program to continue executing when it attempts to access an `array` or `vector` element that does not exist.