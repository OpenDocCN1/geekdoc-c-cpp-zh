```
Enrollment { StudentID = 1, CourseName = Physics, DateEnrolled = 20/07/2021 }
Enrollment { StudentID = 1, CourseName = Chemistry, DateEnrolled = 20/07/2021 }
Enrollment { StudentID = 1, CourseName = Physics, DateEnrolled = 20/07/2021 }
Enrollment { StudentID = 2, CourseName = Physics, DateEnrolled = 20/07/2021 }
False
True
False
```

The comparisons show that Enrollments[0] matches Enrollments[2], but not Enrollments[1] or Enrollments[3]. Remember that records are value types, so the comparison is based on the contents of the records. They are not the same physical record.

+   10. Return to Visual Studio.

+   11. To test the immutability of these records, add the following statement to the doWork method:

Click here to view code image

```
static void doWork()
{
    Enrollments[0].DateEnrolled = new DateOnly(2021, 08, 15);
}
```

+   12. On the Build menu, select Rebuild Solution. The build should fail with the message:

Click here to view code image

Init-only property or indexer 'Enrollment.DateEnrolled' can only be assigned in an object initializer, or on 'this' or 'base' in an instance constructor or an 'init' accessor.

+   13. Delete the statement and rebuild the project. It should build successfully again.

# Summary