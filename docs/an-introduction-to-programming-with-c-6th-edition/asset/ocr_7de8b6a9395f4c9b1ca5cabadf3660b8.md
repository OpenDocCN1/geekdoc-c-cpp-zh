# The Social Security Number Program

```
 //remove any commas or spaces
while (subscript < income.length()) {
    if (income.substr(subscript, 1) == ",") {
        // income.substr(subscript, 1) == ")
        income.replace(subscript, 1, "");
    } else {
        subscript += 1;
        // you can use subscript
        subscript++;
    }
}
```

Figure 13-29 Partial annual income program showing the replace function

# Mini-Quiz 13-3

+   1. Which of the following searches for a comma in a string variable named cityState and assigns the result to an int variable named location
   a. location = cityState.find("

> The answers to Mini-Quiz questions are located in Appendix A.

# The Social Security Number Program

Figure 13-30 shows the program description and IPO chart for the Social Security number program. The program should allow the user to enter a Social Security number without the hyphens. If the user's entry contains nine characters, the program should insert hyphens in the appropriate places in the Social Security number and display the result on the screen. If the user did not enter nine characters, the program should display an appropriate message. You will learn how to insert characters within a string variable in the next section.