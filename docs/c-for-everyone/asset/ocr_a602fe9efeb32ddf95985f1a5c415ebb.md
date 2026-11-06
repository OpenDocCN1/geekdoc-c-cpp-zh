![](bbox=[0.446, 0.093, 0.745, 0.159])

**Figure 4** Class Diagram

A class aggregates another if its objects contain objects of the other class.

The **aggregation** relationship states that objects of one class contain objects of another class. Consider a quiz that is made up of questions. Since each quiz has one or more questions, we say that the class Quiz aggregates the class Question. There is a standard notation, called a UML (Unified Modeling Language) class diagram, to describe class relationships. In the UML notation, aggregation is denoted by a line with a diamond-shaped symbol (see Figure 4).

Finding out about aggregation is very helpful for deciding how to implement classes. For example, when you implement the Quiz class, you will want to store the questions of a quiz as a data member. Since a quiz can have any number of questions, you will choose a vector:

```
```cpp
class Quiz
{
   ...
private:
   vector<Question> questions;
};
```
```

In summary, when you analyze a problem description, you will want to carry out these tasks:

+   - Find the concepts that you need to implement as classes. Often, these will be nouns in the problem description.
+   - Find the responsibilities of the classes. Often, these will be verbs in the problem description.
+   - Find relationships between the classes that you have discovered. In this section, we described the aggregation relationship. In the next chapter, you will learn about another important relationship between classes, called inheritance.

![](bbox=[0.488, 0.674, 0.921, 0.927])

*A car has a motor and tires. In object-oriented design, this 'has-a' relationship is called aggregation.*