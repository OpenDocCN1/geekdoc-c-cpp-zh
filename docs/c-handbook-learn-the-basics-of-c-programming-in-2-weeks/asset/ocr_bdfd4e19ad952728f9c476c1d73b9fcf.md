# Script Mode Programming

If you invoke the interpreter with a script parameter, the script will start to execute and continue to run until it is done. When it is done, the interpreter will not be active anymore. Consider the following example. The sample program is written in a script and has a .py extension:

```
print " Monty Python ' s Flying Circus " ;
```

If you type in the above given source code in a test.py file and run it as

```
$ python test.py
```

you will obtain the following output:

Monty Python ' s Flying Circus

Another way to execute scripts is to modify the .py file, such as:

```
#!/usr/bin/python
```

```
print " Monty Python ' s Flying Circus " ;
```

If you run it as

```
$ chmod + x test.py
```

```
$ ./test.py
```

you get the following output:

Monty Python ' s Flying Circus