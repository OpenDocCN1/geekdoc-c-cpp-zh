
# 3.6 Blocks and variable definitions

It turns out that most C++ programmers would write the average computation program from Section 3.4 slightly differently, as follows.

```
main_program{
    int count;
    cout << "How many numbers: ";
    cin >> count;

    float sum=0;
    repeat(count){
        cout << "Give the next number: ";
        float num;                // defined inside the loop
        cin >> num;
        sum = sum + num;
    }

    cout << "Average is: ";
    cout << sum/count;
    cout << endl;
}
```

As you can see, the only difference is that the variable num is defined inside the loop rather than outside. We first explain how the variable definition is executed in the new program. As you might guess, the variable indeed gets created when control reaches the definition statement. From the time of creation, the variable is available to the program, until the time the control reaches the end of the loop body in the current iteration. In other words, the variable is destroyed when the control reaches the end of the body! Thus, in each iteration of the loop, the variable is created and destroyed. Of course, destroying a variable is only notional, the computer merely assumes that the memory that was given is now available for use. It should also be noted that the variable cannot be used outside the repeat loop, or before its definition inside the loop.

Experienced programmers prefer to write the average computation code in the new style, because in this the definition of num is placed close to its use. Placing definitions close to the use makes it easier to read the program, especially if it has many variables and the loop bodies are large.

Next we will state the general rules for all this. First we need the notion of a block.

## 3.6.1 Block

The region of the program from an opening brace, {, to the corresponding closing brace, }, is called a block. Thus the entire program forms a block, and the body of a repeat also forms a block, which is contained inside the block consisting of the entire program. If there is a repeat inside a repeat, then the block corresponding to the body of the former is contained inside the block associated with the latter. As you can see, two blocks must either

be completely disjoint, or one of them must be completely contained in the other. It is also useful to define the parent block of a variable definition: it is the innermost block in which the variable is defined.

## 3.6.2 General principle 1

Now, we can restate more formally what we stated earlier. When control reaches a variable definition, the corresponding variable is created. The variable is destroyed when the control leaves the parent block of the definition. The variable is potentially available for use in the region of the program starting at the point of its definition, and going to the end of its parent block. This region of the program is called the scope of the definition.

We have already discussed how this principle applies to the variable num of the program given above.

The principle also applies to the variable sum in the program. Its parent block is the main program itself, and indeed, the entire portion of the program from the point of its definition to the end of the program can refer to the variable sum.

## 3.6.3 General principle 2

The principles in giving names to variables and using the names, are somewhat similar to the way in which we give names to human beings.

Let us first discuss how we name human beings. Ideally, you might think that we should insist that all human beings be given different names. But of course, this does not happen. It is perfectly possible that there exist two families in Mumbai both of which name their son Raju. In that case whenever a reference is made to “Raju” in either family, it is deemed to refer to the son in that family. There is no confusion. Notice however, that usually the same name is not given to two children in the same family.

As another example, consider the name Manmohan. In most families in India, the name would be considered to be referring to the Prime Minister of India. Suppose now that a certain family decides to name their son “Manmohan”. In this family, after the birth of the son, if anyone speaks of Manmohan, it would probably be considered as referring to the son. You could say that the son “overshadows” the Prime Minister in this family.

Variable naming in C++ is almost as flexible as naming of human beings, including the idea of shadowing. The analogue of the family is a block of the program.

name Q will not refer to the first variable. It will instead refer to the second variable – unless that of course is shadowed by a third definition of Q.

Here are some examples.

```
main_program{
    int sum=0;
    repeat(5){
        int num;                // statement 1
        cin >> num;
        sum += num;
    }
    cout << sum << endl;
    int prod=1;
    repeat(5){
        int num;                // statement 2
        cin >> num;
        prod *= num;
    }
    cout << prod << endl;
}
```

In this case the references to num in the first loop are in the scope of the definition in statement 1 (and of no other definition), and hence refer to the variable created in statement 1. Similarly the references to num in the second loop are in the scope of the definition in statement 2 (and of no other definition), and hence refer to the variable created in statement 2. This is what you would intuitively expect, and indeed the program will compute the sum of the first 5 numbers that it reads, and the product of the next 5.

Here is an example of a program in which there is shadowing.

```
main_program{
    int p=10;                   // statement 3
    repeat(3){
        cout << p << endl;      // statement 4
        int p=5;                // statement 5
        cout << p << endl;      // statement 6
    }
    cout << p << endl;          // statement 7
}
```

In this program, the occurrence of p in statement 6 is in the scope of the definitions in statements 3 and 5, with the latter shadowing the former. Thus the name p in statement 6 refers to the variable created in statement 5. However, note that the statements 4 and 7 are only in the scope of the definition in statement 3. Thus the name p in this statements refers to the definition in statement 3.

Thus when control arrives at statement 3, a variable p is created. When control arrives at statement 4, the value of this p, 10, is printed. When control arrives at statement 5, a new variable also named p will be created, and will start shadowing the definition of statement 3. At the end of the loop the variable created in statement 5 will be destroyed. Thus when control reached statement 7, the variable created in statement 6 will have been destroyed, and the statement is in the scope only of the definition in statement 3. Thus the reference to p in statement 7 will be considered to be to the variable p defined in statement 3. Thus statement 7 will cause 10 to be printed. Thus the entire code when executed will cause the sequence of numbers 10, 5, 10, 5, 10, 5, 10 to be printed.

## 3.7 Concluding remarks

The initial part of most programs consist of statements which reserve memory in which to store data. Such statements are called variable definition statements. A definition reserves the space and also gives it a name. The reserved space, together with its name, is said to constitute a variable, and the data stored in the variable is said to be the value of the variable. Of course, what is stored in memory is always a sequence of bits. The value represented by the bit sequence depends upon how we interpret the bits, which is specified by the type of the variable. As discussed in Chapter 2, it is possible that the same pattern of 32 bits might mean one value for a variable of type unsigned int, another for a variable of type (signed) int, and yet another for a variable of type float.

When we define a variable, it is always for some specific purpose. So it is strongly recommended that the name chosen for the variable reflect that purpose. Also, along with the definition, it is useful to write additional comments which explain its purpose in more detail if necessary.

When we refer to the name of a variable in a program, we almost always refer to the value stored in the variable, except when the name appears on the left side of an assignment statement, when it refers to the memory associated with the variable, i.e. whatever is the value on the right hand side is to be stored in this memory. Perhaps this observation is useful to prevent being confused by statements such as p = p + 1; which are incorrect in mathematics but which are meaningful in computer programs. We also noted that the assignment statement is somewhat subtle, because of issues such as rounding, and converting between different types of numbers.

The assignment statement also plays a central role in two important programming idioms: sequence generation, and accumulation. We saw a number of operators which can be considered to have been inspired by these idioms.

We noted that it is convenient if a variable is defined close to the point in the program where it is used. This led us to notion of the scope of a variable, i.e. the region of the program where the variable can be referred to, and also the notion of shadowing.

## 3.8 Exercises

1. What is the value of x after the following statements are executed? (a) x=22/7; (b) x=22.0/7; (c) x=6.022E23 + 1 - 6.022E23 (d) x=6.022E23 - 6.022E23 + 1 (e) x=6.022E23 * 6.022E23. Answer for three cases, when x is defined to be of type int, float, double. Put these statements in a program, execute and check your conclusions.
