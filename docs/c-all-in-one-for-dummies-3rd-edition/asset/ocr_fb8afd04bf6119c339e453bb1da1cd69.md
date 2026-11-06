# And now the answer to The Great Question

In C++, as well as in the original C language (upon which C++ is based), the operator ++ adds 1 to a variable. So this finally brings us to a point where we can answer The Great Question: Where did the name C++ come from? When the guy who originally designed C++, Bjarne Stroustrup, needed a name for his language, he decided to look into its roots for the answer. He had based the language on C; and in C, to add 1 to something, you use the ++ operator. And because he felt that he added only 1 thing to the language, he decided to call the new language C++. Okay, that’s not

quite true; Bjarne actually added a great deal to the language. But that entire great deal can be thought of as just one thing made of lots of smaller things. What did he add? The main thing of those smaller things is the capability to do object-oriented programming. That’s something we cover in the next chapter. And by the way, the originator of C++, Mr. Stroustrup, is still alive and still doing work for the language at AT&T. You can see his web page at

http://www.research.att.com/~bs

Table 3-3 summarizes the different things you can do that involve the addition of variables.

| Table 3-3 | Doing Things with Addition |
|---|---|
| *What You Can Do* | *Sample Statement* |
| Add two variables | `cout << start + time << endl;` |
| Add a variable and a number | `cout << start + 5 << endl;` |
| Add two variables and save the result in a variable | `total = start + time;` |
| Add a variable and a number and save the result in a variable | `total = start + 5;` |
| Add a number to what’s already in a variable | `total = total + 5;` |
| Add a number to what’s already in a variable by using a shortcut | `total += 5;` |
| Add a variable to what’s already in a variable | `total = total + time;` |
| Add a variable to what’s already in a variable by using a shortcut | `total += time;` |
| Add 1 to a variable | `total++;` |