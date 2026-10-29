```
if (num == 5)
    cout << "Bingo!\n";
else
    cout << "Bongo!\n";

return 0;
}
```

Program 4.7 has two paths that can be traversed as the program progresses from its opening brace to its closing brace. The first path, which is executed when the input number is 5, is in this sequence:

```
cout << "Enter a number";
cin >> num;
cout << "Bingo!\n";
```

The second path, which is executed when any number except 5 is input, includes this sequence of instructions:

```
cout << "Enter a number";
cin >> num;
cout << "Bongo!\n";
```

Testing each possible path through Program 4.7 requires two runs with a judicious selection of test input data to make sure both paths of the if statement are exercised. Adding one more if statement in the program increases the number of possible execution paths by a factor of two and requires four (that is, 2²) runs for complete testing. Similarly, a program consisting of three unnested if-else statements requires eight (that is, 2³) runs for complete testing, and a program containing four unnested if-else statements requires 16 (that is, 2⁴) test runs.

Now consider a program consisting of only 10 modules, with each module containing five if statements. Assuming the modules are always called in the same sequence, there are 32 possible paths through each module (2⁵) and more than 1,000,000,000,000,000 (2⁵⁰, representing the number of modules multiplied by the number of if statements per module) possible paths through the complete program (all modules executed in sequence). The time needed to create test data and the computer runtime required to exercise each path with the test data make complete testing of this program virtually impossible.

The inability to test all combinations of statement execution sequences fully has led to the programming proverb "There is no error-free program." It has also led to the realization that any testing should be well thought out to maximize the possibility of locating errors. At a minimum, test data should include suitable values for input data, illegal input values that the program should reject, and limiting values that are checked by selection statements in the program.