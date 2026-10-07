# Introduction to Language Integrated Query (LINQ)

For more complicated lambda expressions, a statement block should be adopted. An example of this kind of syntax is shown below:

```
(x, y) => { if (x > y) return x; else return y; }
```

One point to be noticed is that the data type of both the input and the output parameters must be identical with those types defined in the delegate. For example, in the previous sample x => y, if the input is defined as a string and the output is defined as an integer by the delegate, the output must be converted to an integer by using the following lambda expression:

```
x => y.Length
```

Where Length is a method to convert the string to an integer. Another example of using lambda expressions to perform LINQ query is:

```
IEnumerable<Faculty> faculty = EnumerableExtensions.Where(faculties, f => f.faculty_name == "Ying Bai");
```

Here the Query Operator method Where is used as a filter in query. The input is an object with a type of faculties, and the output is a string. The compiler is able to infer that "T" to a faculty because the first parameter of the Where() method is IEnumerable<Faculty>, that T must, in fact, Faculty. Using this knowledge, the compiler also verifies that Faculty has a faculty_name member. Finally, there is no return keyword. In the syntactic form, the return member is omitted but is merantically convenient. The result of the expression is still considered to be the return value.

Lambda expressions also support a more verbose syntax that allows you to specify the types explicitly, as well as execute multiple statements. An example of this kind of syntax is:

```
return EnumerableExtensions.Where(faculties, Faculty f) => {string id = faculty_id; return f.faculty_id = id};
```

Here the EnumerableClasses allows us to access and use the static method Where() since all Standard Query Operator are static methods defined in Enumerable or Queryable classes. As you know, a static method is defined as a class member and can be accessed by each class in that method is defined. Is possible for us to access a static method from an instance of that class? Generally, this will be considered as a stupid question since that is impossible. Is there any way to make it possible? The answer is yes. To get that answer correctly, let's go to the next topic.

# 4.9.2 EXTENSION METHODS

Regularly, static methods can only be accessed and used by classes in which those static methods are defined. For example, all Standard Query Operator methods, as we discussed in Sections 4.1.3 and 4.1.4, are static methods defined in Enumerable or Queryable classes and can be accessed by those classes directly. But those static methods cannot be accessed by any instance of those classes. Let's use an example to make this story.

Figure 4.1 shows a pieces of code that defines both class and instance methods. In this example, the method ConvertToUpper() is an instance method and ConvertToLower() is a class method. To call them, a different calling strategy must be utilized. To call and execute the instance method ConvertToUpper(), one must first create a new instance of the class Conversion, and then call that method. To call and execute the class method ConvertToLower(), one can directly call it