# Understanding how computers use loops

Suppose that you’re writing an application to add all the numbers from 1 to 100. For example, you may want to know how much money you will get if you tell 100 people, “Give me one dollar more than the person to your left.” With a mastery of copy-and-paste, you could do something like this (with the first person giving you a dollar, the second giving you two dollars, the third giving you three dollars, and so on):

```
int x = 1;   // First person.
x = x + 2;   // Person two gives you 2, for a total of 3
x = x + 3;   // Person three gives you 3, for a total of 6
x = x + 4;   // Person four gives you 4, for a total of 10
```

and so on until you get to x = x + 100. As you can see, this code could take a long time to type, and you would probably find it a tad frustrating, too, no matter how quickly you can choose the Edit➜Paste command (or press Ctrl+V). Fortunately, the great founders of the computer world recognized that not every programmer is a virtuoso at the piano with flying fingers and that applications often need to do the same thing over and over. Thus, they created a helpful tool: the for loop. A for loop executes the same piece of code repeatedly a certain number of times. And that’s just what you want to do in this example.

# Looping situations

Several types of loops are available, and in this section you see how they work. Which type of loop you use depends on the situation. The preceding section meth- ods one loop type: the for loop. The idea behind a for loop is to have a coun- ter variable that either increases or decreases, and the loop runs as long as the counter variable satisfies a particular condition. For example, the counter variable might start at 0, and the loop runs as long as the counter is less than 10. The counter variable increments (has one added to it) each time the loop runs, and after the counter variable is less than 10, the loop stops.

Another way to loop is to simplify the logic a bit and say, “I want this loop to run as long as a certain condition is true.” This is a while loop, and you simply specify a condition under which the loop continues to run. When the condition is true, the loop keeps running. After the condition is no longer true, the loop stops.

Finally, there’s a slight modification to the while loop: the do-while loop. The do-while loop is used to handle one particular situation that can arise. When you have a while loop, if the condition is not true when everything starts, the computer skips over the code in the while loop and does not even bother executing