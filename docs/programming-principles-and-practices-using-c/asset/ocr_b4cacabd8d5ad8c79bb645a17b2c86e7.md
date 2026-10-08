```
if (!in>=ws).eof() error("characters after total line");
return 0;
}
// update totals:
boys += curr_boy;
girls += curr_girl;
}
error("didn't find total line");
}
```

The last row is semantically different from the other rows — it is their sum. We recognize it by its label (“Alle klasster”). We decided to accept no more non-whitespace characters after that last one (using the technique from \textbf{to->o}; \S23.2) and to give an error if we did not find it.
We used \textbf{from string()} from \S23.2 to extract an integer value from the data fields. We had already checked that those fields consisted exclusively of digits so we did not have to check that the \textbf{string-to-int} conversion succeeded.

# 23.10 References

Regular expressions are a popular and useful tool. They are available in many programming languages and in many formats. They are supported by an elegant theory based on formal languages and by an efficient implementation technique based on state machines. The full generality of regular expressions, their theory, their implementation, and the use of state machines in general are beyond the scope of this book. However, because these topics are rather standard in computer science curricula and because regular expressions are so popular, it is not hard to find more information (should you need it or just be interested).
For more information, see:

Aho, Alfred V., Monica S. Lam, Ravi Sethi, and Jeffrey D. Ullman. Compilers: Principles, Techniques, and Tools, Second Edition (usually called “The Dragon Book”). Addison-Wesley, 2007. ISBN 0321547985.

Cox, Russ. “Regular Expression Matching Can Be Simple and Fast (but Is Slow in Java, Perl, PHP, Python, Ruby, …)” http://swtch.com/~rsc/regexp/regexp1 .html.

Maddock, J. boost:regex documentation. www.boost.org/.

Schwartz, Randal E., Tom Phoenix, and Brian D. Foy. Learning Perl, Fourth Edition. O’Reilly, 2005. ISBN 0596101058.