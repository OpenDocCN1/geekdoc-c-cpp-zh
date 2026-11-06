(Note that the second and third lines begin with a single tab; do not start the first line with any tabs.) Next, make a text file in the same directory and call the file `test.txt`. Finally, while in the same directory, type the following command:

```
make
```

Note that you will need to have a make command installed. For example, you can obtain Cygwin at http://www.cygwin.com/. Book VI, Chapter 4 describes the Boost.Build compiler. You can also obtain the Borland compiler from http://www.embarcadero.com/downloads.

![](bbox=[0.148, 0.274, 0.228, 0.325])

If you do some exploring, you are likely to discover that you can, optionally, name your Makefile something other than Makefile and then specify your filename in the make command. For most versions of make, you do this by typing

```
make -f filename
```

However, we do not recommend doing this. Most programmers always use the filename Makefile, and if you call yours something different, you are likely to rattle their chains a little. Computer people are not known for their flexibility; and if you do this, your coworkers probably won't pay for your pizza this Friday.

# Using rules that depend on other rules

Some special situations arise when working with inference rules. For example, `test.out` may not exist at all. In that case, the commands will definitely run because the idea is that this rule tells how to create a `test.out` file.

Another special situation deals with `test.txt` itself in the previous examples. Does *it* depend on anything? For example, another rule may say this:

```
test.txt: originalfile.txt
	cp originalfile.txt test.txt
```

This rule states that `test.txt` depends on `originalfile.txt`. If `originalfile.txt` has changed, make creates `test.txt` based on the command, which is a `cp` command.

As it turns out, make is surprisingly smart for such an old computer tool. Before it ventures into the rule to create `test.txt`, it sees that `test.txt` depends on `originalfile.txt`, and checks to see whether `originalfile.txt` has any rules. If so, make keeps tracing backward until it gets to a rule with no prior dependencies.