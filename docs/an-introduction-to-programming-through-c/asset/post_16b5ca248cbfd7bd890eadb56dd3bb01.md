
## Chapter 9
### Functions

In the preceding chapters, we have seen programs to do many things, from drawing polygons and miscellaneous pictures to calculating income tax and finding the greatest common divisor (GCD) and finding roots. It is conceivable that we will want to write more and more complex programs in which some of these operations, e.g. finding the GCD, is needed at many places. One possibility is to copy the code for the operation in as many places as is required. This doesn't seem too elegant, and is also error prone. Wouldn't it be nice, if for each frequently used operation you could somehow construct a "command" that could then be used wherever you want in your program? Just as we have a command sqrt for computing the square root, or commands to compute the trigonometric ratios (Section 1.5) can we build a gcd command that will compute the GCD of two numbers when demanded? This can be done, and how to build such commands is the subject of this chapter.

The term function is used in C++ to denote what we have so far informally called a command. In some languages the terms procedure or subprogram are also used. In what follows, we will use the term function.

### 9.1 Defining a function

Suppose that we indeed need to frequently compute the GCD, and so would like to have a function which computes this. It is natural to choose the name gcd for this function. It could take two numbers as arguments, and return their GCD, which could then be used. As an example, suppose you wanted to find the GCD of 24 and 36, and also the GCD of 99 and 47. If we had a gcd function as described, then we could write a very simple main program as follows.

```
main_program{
    int a=36,b=24,c=99,d=47;
    cout << gcd(a,b) << endl;
    cout << gcd(c,d) << endl;
}
```

Since we don't already have such a gcd function, we must define it. We discuss how to do this next.

```
int gcd        // return-type function-name
(int m, int n)  // parameter list: (parameter-type parameter-name ...)
{
// beginning of function body
    while(m % n != 0){
        int Remainder = m % n;
        m = n;
        n = Remainder;
    }
    return n;
}
// end of function body
```

Figure 9.1: Definition of a function to compute the GCD

Basically, in the definition, we must specify what needs to happen when the function is called during execution, e.g. for the call gcd(a,b) in the main program above. In essence, the idea is to have a small program run, sort of in the background, for computing the GCD. This program, which we will refer to as a subprogram must be given the inputs, (in the present case, the values of the numbers whose GCD is to be computed), and some mechanism must be established for getting back the result (in the present case the computed GCD) of the computation to the main program. While the sub-program runs, the main program must simply wait.

Figure 9.1 shows the code for defining gcd. The simplest way to use the definition is to place it in the same file as the main program given earlier, before the main program. If you compile and run that file, then it will indeed print 12 and 1, the GCD respectively of 24, 36 and 99, 47, as you expect. The requirement that the function definition be placed before the main program is similar to the requirement that a variable must be defined before it is used. We can relax this requirement slightly, as will be seen in Section 11.2.7.

In general, a function definition has the form:

```
type-of-return-value function-name (parameter1-type parameter1-name,
parameter2-type parameter2-name, ...){
body
}
```

The definition begins with type-of-return-value, which indicates the type of the value returned by the function. In the GCD example, the function computes and evaluates the GCD, which has type int, so our definition (Figure 9.1) mentions this.

Next is function-name, the name of the function being defined. In our example, we chose to call our function gcd, so that is what the code states. Any valid identifier (Section 3.1.1) can be chosen as a function name.

that can be present in a main program. However, there are two additional features. The code in the body can refer to the parameters, as if they are variables. Further, the the body must contain a return statement, which we explain shortly. We note that the body of the definition in Figure 9.1 is taken substantially from the program developed in Section 7.7.

### 9.1.1 Execution: call by value

Consider our gcd function and main program. While executing the main program, suppose that control arrives at the call gcd(a,b). We describe the general rule that determines what happens, and also mention what happens in our specific case.

- 1. The arguments to the call are evaluated. In our case it simply means fetching the values of the variables a,b, viz. 36,24. But in general, the arguments could be arbitrary expressions which would have to be evaluated.
- 2. The execution of the calling subprogram, i.e. the subprogram which contains the call, main_program, in this case, is suspended. The calling subprogram will be resumed later. When resumed, the execution will continue from where it was suspended.
- 3. Preparations are made to start running a subprogram. The subprogram will execute the code given in the body of the function. The subprogram must be given a separate area of memory so that it can have its own variables. It is customary to refer to this area as the activation frame of the function call. Immediately, space is allocated in the activation frame for storing the variables corresponding to the parameters of the function.
  
  Thus in our case, an activation frame is created corresponding to the call gcd(a,b). The gcd function has two parameters, L, S. So variables, L and S will be created in the activation frame.
- 4. The value of the first argument is copied to the memory associated with the first parameter. The value of the second argument to the second parameter, and so on.
  
  Thus, in our case, 36 will be copied into the variable L, and 24 into the variable S in the activation frame created for the call gcd(a,b). Figure 9.2(a) shows the state of the memory at this time. We have referred to the memory area used by main_program as its activation frame. This is customary.
- 5. Now the body of the called function is executed. The body must refer to variables or parameters stored only in the activation frame of the call.1 If space needs to be reserved for variables etc., it is done only inside the activation frame of the call.
  
  Thus in case of our program, the code may refer to the parameters L, S. The code cannot refer to variables a,b,c,d because they are not in the activation frame of gcd(a,b). When the first statement of the body is executed, it causes the creation of the variable Remainder. The space for this is allocated in the activation frame of the call. Such variables are said to be local to the call.

1 We will modify this a bit later.

6. The body of the function is executed until a return statement is encountered. The expression following return is called the return-expression and its value is sent back to the calling program. The value sent back is considered to be the value of the call in the calling program.

In our case the execution of the function happens as follows. In the first iteration of the loop, L, S have values 36,24. At the end of this iteration, the values become 24,12. The state of the memory at this point is shown in Figure 9.2(b). In the next iteration, Remainder becomes 0, and so the break statement is executed. Thus the control exits from the loop, and return is reached. The return-expression is S which has value 12. This value is sent back to the calling program.

7. The activation frame created for the call is not needed any longer, and is destroyed, i.e. that area is marked available for general use.

8. The calling program resumes execution from where it had suspended. The returned value is used as the value of the call itself.

In our case the call was gcd(a,b), and its value is required to be printed. Thus the value returned, 12, will be printed. After this the next cout statement will be executed (in which we will encounter the second call to gcd). This will cause an activation frame to be created again etc.

In this model of executing function calls, only the values of the arguments are sent from the calling program to the called function. For this reason, this model is often termed as call by value. We will see another model later on.

It is worth considering what happens on the second call to gcd, i.e. the call gcd(c,d) in the code. The same set of actions would repeat. A new activation frame would be created for this call, and very likely it would use the same memory as was used for the activation frame of the previous call. The point to be noted is that each call requires some additional memory, but only for the duration of the execution of the call.

### 9.1.2 Names of parameters and local variables

We have already said that when a function call executes, it can only access the variables (including the parameters) in its activation frame. In particular, the variables in the calling program (in this case main_program) cannot be accessed. So it is perfectly fine if variables in the calling program and the called function have the same name! Note further that when the calling program is executing, the activation frame of the called function does not even exist, so there is no question of any confusion.

### 9.2 Nested function calls: LCM

Suppose now that you wish to develop a program to compute the least common multiple (LCM) of two numbers. This is easily done using the following relationship between the LCM, L, and the GCD, G of two numbers m, n:

L = (m × n) / G
