# 8.8 Case Study: GradeBook Using an Array to Store Grades

```
// multiply argument by 2
static void ModifyElement(int element)
{
    element *= 2;
    Console.WriteLine($"Value of element in ModifyElement: {element}");
}
```

Effects of passing reference to entire array:
The values of the original array are:

+   1 2 3 4 5

The values of the modified array are:
2 4 6 8 10

Effects of passing array element value:
array[3] before ModifyElement: 8
Value of element in ModifyElement: 16
array[3] after ModifyElement: 8

> Fig. 8.13 | Passing arrays and individual array elements to methods. (Part 2 of 2.)

8.13 next demonstrates that when a copy of an individual value-type element is passed to a method, modifying the copy in the called method does not affect the original value of element in the calling's method. To show the value of array[3] before invoking ModifyElement, lines 30–31 display the value of array[3], which is 8. Line 33 calls ModifyElement (lines 47–51) passes array[3] as an argument. Remember that array[3] is actually one int (8) in array. Therefore, the app passes a copy of the value of array[3]. Method ModifyElement multiplies the value received as an argument by 2, results then outputs the value of element (16). Since method parameters, like local variables, cease to exist when the method in which they are declared execution, the method parameter element is destroyed when ModifyElement terminates. When the app returns to Main, line 34 displays the unmodified value of array[3] (i.e., 8).

# 8.8 Case Study: GradeBook Using an Array to Store Grades

We now present the first version of a GradeBook that instructors can use to maintain students' grades on an exam and display a grade report that includes the grades, class average, lowest, highest grade and a grade distribution chart. The version of GradeBook presented in this section stores the grades for one exam in a one-dimensional array. In Section 8.10, we present a second version of GradeBook that uses a two-dimensional array to store students' grades for several exams.

Storing Grades in an array in class GradeBook

Figure 8.14 shows how the output summarizes the 10 grades we store in an object of class GradeBook (Fig. 8.15), which uses an array of integers to store the grades of 10 students for a single exam. The array is declared as an instance variable in line 7 of Fig. 8.15—therefore, each GradeBook object maintains its own set of grades.