# The Plano Elementary School Program

(continued)

```
43 else
44     cout << "Sorry, the correct answer is "
45      << correctAnswer << ".";
46     //end if
47     cout << endl << endl;
48  }
49     //end for
50     system("pause");
51     return 0;
52 } //end of main function
53 
54 /********function definitions*****
55 int getRandomNumber(){
56 {
57     int randInteger = 0;
58     //generate random integer from 1 through 10
59     randInteger = 1 + rand() % (10 - 1);
60     return randInteger;
61 } //end of getRandomNumber
```

333

![](bbox=[0.433, 0.211, 0.574, 0.252])

![](bbox=[0.608, 0.329, 0.656, 0.363])

Figure 9-18 Modified random addition problems program

# The Plano Elementary School Program

The principal of Plano Elementary School would like to use the random addition program that you completed in the previous section. However, she wants the ability to specify the range of random numbers that appear each time the program runs. This will require you to make a few modifications to the program to allow the user to enter the smallest and largest integer in the desired range. You will then have the function calls in the program send that information to the **getRandomNumber** function. Figure 9-9 shows the Plano Elementary School Program. The changes made to the code are shown in Figure 9-19. The Plano Elementary School program provides an example of code. It also demonstrates how you can improve programming productivity by splitting larger problems into a series of smaller problems. Each small problem can be assigned to a member of the programming team. In this case, you can handle the **main** function while your friend Sam gets the matter, **getRandomNumber** function. By splitting the work in this manner, you won't need to worry about the code for generating random numbers. However, the stat in function needs a random number. Actually, you can use Sam's function in any program that requires a random integer within a specific range; you just need to enter the function definition in the program. (Depending on your prototype.) Sam will also be using another programmer's code in C++. More specifically, he'll be using the C++ built-in **rand** function. Figure 9-20 shows a sample run of the Plano Elementary School Program.