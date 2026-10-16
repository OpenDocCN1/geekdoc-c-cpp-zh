
With the introduction of Objective-C 2.0, and its fast enumeration capabilities, the for loop has become really the primary loop choice when working in Objective-C. However, the while and do-while loops serve important functions in the language.

## Working with for

The for loop is probably the most commonly used loop in Objective-C. Using it, you can count over a range of numbers, iterate over an array of items, and so on. Because of this flexibility, some variations in its syntax can be confusing.

### Traditional for loops

The first variation of the for loop that I would like to introduce to you is the traditional form. In this form, a for statement consists of the statement followed by the conditions of the for loop in the form of three statements inside parentheses. These three statements correspond to the three operations that are performed on the control variable as the for loop executes. The first operation sets the initial conditions of the control variable, and it is typically used to initialize the variable to zero, or in the case where you don't want to start counting at zero, to some other value. This first operation is only executed the first time the for loop is entered.

The second operation is the conditional statement that is evaluated upon each iteration of the loop to determine if the loop should be halted. If the conditional statement is evaluated to be true, then the for loop is interrupted and program execution continues after the for loop code block. If the conditional statement is evaluated to be false, another iteration of the for loop code block is executed.

The final operation is the counting expression. It is this expression that is used to actually change the value of the control variable for each iteration of the loop. During each iteration, the control variable can be incremented, decremented, assigned to, and so on at will in the counting expression.

Listing 2.35 shows an example of a typical for loop.

### Listing 2.35

#### A for loop

```
for(int i = 0; i < 100; i++)
{
  Foo *foo = [array objectAtIndex:i];
  [foo doSomething];
}
```

In this case, the first time that the for loop is entered, the control variable (i) is created and assigned a value of zero. On each iteration of the loop, the conditional expression is evaluated to determine if the control variable has reached 100. If it has, execution will jump to the statement directly after the for loop code block. If it has not, then the counting expression is executed; in this case, the control variable is incremented by one.

NOTE

Your counting expression can be anything you want it to be. For example, to increment a loop that counts by twos, you could simply increment your control variable by two in each iteration of the loop instead of by one like we are doing here.

NOTE

The x++ operator is the postfix increment operator. It increments the value of x and stores it back into x. When doing so, it also returns the value of x before it has been incremented. The ++x operator is the prefix increment operator. It also increments the value of x and stores it into x, but the value it returns is the value of x after the increment. The same goes for the post/pre versions of the decrement operator, --. In some cases, you may want to assign the return value of these operations to another variable. When doing so, be aware of this behavior.

The control variable is available within the scope of the for loop code block and can be used, for example, to reference indexes within arrays or to drive conditional logic within the for loop code block. Additionally, a for loop can be aborted at any time within the for loop code block by executing a continue statement. The continue statement will stop execution of the for loop immediately and reset execution back to the beginning of the loop. An example of this is shown in Listing 2.36.

### Listing 2.36

#### The continue statement

```
for(int n = 0; n < 100; ++n)
{
    if(n > 10 && n < 20)
        continue; // this skips 11-19
    // do something with n...
    Foo *foo = [array objectAtIndex:i];
    [foo doSomething];
}
```

### Using for for fast enumeration

The second form of for loops is a new addition in Objective-C 2.0; it applies to enumerating over objects contained in collections. You learn about collections and objects in the next chapter, but I want to introduce you to the fast enumeration syntax here so you'll be familiar with it when we come to it.

In the previous form of the for loop, we had to use the control variable to retrieve an element of the array in order to operate on it. The fast enumeration form of the for loop obsoletes this mechanism by providing us with an ability to specify, as part of the for statement itself, a temporary variable to store the elements of the collection that is being iterated over. This is tremendously convenient, because the vast majority of for loops are written specifically for the purposes of iterating over the members of a collection and performing an operation on each of the members individually.

An example of a fast enumeration for loop is shown in Listing 2.37.

As you can see, a variable (object) is declared as part of the for statement itself. As the for loop is executed, each member of the collection (array) is assigned to the variable. It is then available within the scope of the for loop code block.

### Listing 2.37

#### For loop with fast enumeration

```
for(Foo *object in array)
{
    // the Foo object is assigned to an element of the array
    // do something with object
}
```

You’ll see a pattern with for loops in use a great deal when I describe collection objects in Chapter 13. For now, simply be familiar with the form of the for loop, and be prepared to return to this chapter again for review.

## Working with while

While loops work similarly to for loops with the exception of the fact that there are not multiple statements inside the parentheses after the while statement. A while statement has a conditional statement which is checked upon each iteration of the loop. When the conditional statement is found to be false, execution continues at the next statement after the end of the while code block.

An example of a while statement is shown in Listing 2.38.

### Listing 2.38

#### While loop

```
int x = 0;
while(x < 10)
{
    NSLog(@"Value of x: %ld", x);
    x++;
}
```

The implication of this sort of control flow is that whatever condition you are checking within the while’s conditional statement needs to, at some point, change to false within the while’s code block. If it doesn’t, your while statement will continue to loop forever. Whiles can also be interrupted with a continue statement just like a for loop.

NOTE

If the conditional statement is false upon the first run of the loop, the code within the while code block will never execute.

While statements are particularly convenient in cases where you have complex iterative logic involved.

Older versions of Objective-C did not have the fast enumeration capabilities that are available today. As a result, the while statement is often used to iterate over arrays using an NSEnumerator. An example of this is shown in Listing 2.39.

### Listing 2.39

#### Old-style enumeration

```
NSArray *someArray = [self getArray];
NSEnumerator *enumerator = [someArray objectEnumerator];
while((NSObject *obj = [enumerator nextObject]))
{
    // do something with obj...
}
```

You rarely see this pattern used today, but because it is so ubiquitous in older code, familiarizing yourself with this concept is important. Each time the conditional statement is checked, the enumerator returns the next object from the array. When it reaches the end of the array, it returns nil. This causes the while conditional to return false. This, in turn, causes execution to jump to the next line of code after the while code block.

## Using do

The final type of loop that we are going to talk about in this section is the do-while loop. This loop is similar to the while loop, with the exception of the fact that the conditional is moved to the end of the loop so that no matter what, at least one iteration through the loop is executed before the conditional is checked. An example of this kind of loop is shown in Listing 2.40.

This loop is one that is rarely used, but when it is, it’s usually an ideal solution to the problem that you’re trying to solve.

### Listing 2.40

#### do-while loop

```
int x = 0;
do
{
    NSLog(@"%ld", x);
    x++;
}
while(x < 10)
```

Usually, this loop is used in cases where you are dealing with some type of control variable that is in a pre-existing state, which you do not want to change until the loop has executed at least once. You may also use this loop when calculating the control variable within the scope of the control block. Again, you might be doing some kind of complex logic in order to arrive at the value of the control variable. The do-while loop gives you an opportunity to perform whatever complex logic you desire inside of its code block before the while conditional is evaluated. Note, however, that the control variable must be declared outside the scope of the do-while code block in order to be within scope for the while conditional.

NOTE

Remember, when dealing with a switch, that it was possible to break out of the switch by using a break statement. This is very common in switch usage. However, break can also be used with do-while, while, and for loops. When used in these contexts, it causes the thread of execution to jump out of the loop to the next line of the program after the loop’s code block.
