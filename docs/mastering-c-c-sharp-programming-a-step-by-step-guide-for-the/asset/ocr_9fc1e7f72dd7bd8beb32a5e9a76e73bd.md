# # Decision-making

All computer programs that do anything considered as real work will need to make decisions somewhere along the line. The decisions will be based on whether specified conditions are met or not. In other words, specific parts of the code will only be run when a state or condition is met. The core of this decision-making process is a C# statement known as the ‘if statement’ as well as a few related ones. We’ll start with the basic if statement, look at the related ones and then move on to look at how we can use them to compare values. We’ll finish by looking at logical operators, special operators used for making more complex conditions.



Imagine a situation where you are a teacher; you have grades to assign and you want to know what grade each student should be given based on their test scores. This is easy to do in the real world and also provides us with an easy example that uses decision-making.

The process the teacher follows is to consider the score for a student; if it is 90 or above, an A grade is awarded; 80 to 90 is a B grade and so on, right down to outright fail. To do this, decisions must be made, and those decisions are based on specific conditions. When we say something is done conditionally, we mean that it is only done some of the time.

Some of the students get an A, some will get a B, some will get a C, and some will fail.

What we are going to do is create a program that takes the student score and uses it to determine the grade. We’ll start at the very beginning.

In C#, the if statement is used to let you check if two things are equal and it will look like this:

```
if(score == 100)
{
}
```