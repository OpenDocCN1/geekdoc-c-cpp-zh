
libraries so that the link editor can link the library. In addition, the table of contents is an archive member at the beginning of the archive that indicates which symbols are defined in which library members.

## The nm Command

The `nm` command displays the symbols that are defined or referenced in a static library. For example, suppose that the library `HelloWorld.a` contains the object file `HelloWorld.o`.

If you type the following command:

```
nm HelloWorld.a
```

The output will be something like this:

```
HelloWorld.a(HelloWorld.o):
0000000000000308 s EH_frame0
0000000000000030 s L_.str
0000000000000000 T _main
0000000000000320 S _main.eh
    U _printf

HelloWorld.a(FindChar2.o):
0000000000000420 s EH_frame0
00000000000000c6 s L_.str
00000000000000d2 s L_.str1
00000000000000de s L_.str2
0000000000000f5 s L_.str3
0000000000000000 T _findChar
0000000000000438 S _findChar.eh
    U _printf

HelloWorld.a(FindMain2.o):
0000000000000440 s EH_frame0
00000000000000c0 s L_main.str1
00000000000000c6 s L_main.str2
00000000000000d4 s L_main.str3
U __stack_chk_fail
U __stack_chk_guard
U _findChar
0000000000000000 T _main
0000000000000458 S _main.eh
```

The letter `U` in the second column in the preceding output indicates that the function specified on the right side of `U` is referenced in the associated `.o` file, and that its definition is located in a different archive library or object file.

## Some Simple Makefiles

This section contains a makefile that does not involve any compilation of C programs. It contains simple rules that execute simple commands. Note that you must use the `-f` switch because of the non-standard filename.

Listing A.1 displays the contents of `Simplemake` that contains a top-level “target” called `all`. This target specifies three other targets for executing Unix commands.

### Listing A.1: Simplemake

```
all: hello now mymakefiles

hello:
	echo "hello world"; echo

now:
	@echo "now is `date`"; echo

mymakefiles:
	@echo "mymakefiles: `ls *akefile*`"; echo
```

Listing A.1 defines the target `all` that specifies the three targets called `hello`, `now`, and `mymakefiles`. Invoking the make utility by specifying the file `Simplemake` will cause all three targets to be invoked, simply by typing the following command:

```
make -f Simplemake
```

The output from my system is shown here:

```
echo "hello world"; echo
hello world

now is Wed May 23 22:50:28 PDT 2018

mymakefiles: Makefile
Makefile-ori
Makefile1
Makefile2
Makefile3
Makefile4
Makefile5
Makefile6
Makefile7
Makefile8
Makefile9
```

If you only want to invoke the first target, then type the following command:

```
make -f Simplemake hello
```

The output from my system is shown here:

```
echo "hello world"; echo
hello world
```

If you only want to invoke the second target, then type the following command:

```
make -f Simplemake now
```

The output from my system is shown here:

```
now is Wed May 23 22:50:28 PDT 2018
```

Finally, if you only want to invoke the third target, then type the following command:

```
make -f Simplemake mymakefiles
```

Keep in mind one thing: the preceding target will list the files containing the string `akefile`. Hence, this target will not list makefiles that do not match this pattern, such as `mymake`, `mymakefile`, `yourmakefile`, and so forth.

With the preceding example in mind, let’s look at an example of a makefile that involves compiling a C program, as discussed in the next section.

## A Makefile for C Programs

Recall that Chapter 1 contains the C program `HelloWorld.c` that you compiled with the following command:

```
gcc HelloWorld.c -o HelloWorld
```

The equivalent functionality of the preceding command involves creating a simple target in a makefile, which is displayed in Listing A.2.

### Listing A.2: Makefile

```
hello: HelloWorld.c
	gcc HelloWorld.c -o HelloWorld
```

Listing A.2 defines the target `hello`, but you can use whatever name is convenient for you.

Now place the Makefile in Listing A.2 and the C program `HelloWorld.c` in the same directory, and then launch the make utility from the command line, just as you did in the previous section. Although no output is displayed, you will see the binary file `HelloWorld` appear in the same directory; launch this file and you will see the following output:

```
Hello World
```

A Makefile often contains multiple targets and can include other constructs such as macro definitions and also reference other makefiles. Keep in mind that the files that are specified on the right-side of the colon are the dependencies, which is `HelloWorld.c` in this example. The second line has a tab-based indentation that is required for any target in a makefile but is not visible in this example. If you use spaces instead of a tab, you will see the following type of error message when you invoke the make utility:

```
Makefile1:13: *** missing separator (did you mean TAB instead of 8 spaces?). Stop.
```

This is one of the most common errors that developers make when they create makefiles.

> **NOTE** The first character in a rule line must be a tab character.

A very simple makefile with the preceding target is discussed in the next section.

## Big Make and Little Make

As you saw earlier in this Appendix, the file `Makefile` is called “big make” and the file `makefile` is called “little make.” If you type `make` on the command line, it will search for “big make” and execute the first target in that makefile. If “big make” does not exist, the make utility searches for “little make” and execute the first target in that makefile.

For example, if the `hello` target is defined in either `Makefile` (such as the one in Listing A.2) or `makefile`, you can invoke that target as follows:

```
make hello
```

As a reminder, if `Makefile` and `makefile` do not exist and you invoke the preceding command, the following message is printed:

```
make: *** No rule to make target `hello'. Stop.
```

## A Makefile with Macros

Listing A.3 displays the contents of `Makefile2` that contains two macro definitions and three targets, all of which create the binary executable `HelloWorld`.

### Listing A.3: Makefile2

```
CC=gcc
CFLAGS=-g -Wall

hello: HelloWorld.c
	gcc HelloWorld.c -o HelloWorld

hello2: HelloWorld.c
	gcc -g -Wall HelloWorld.c -o HelloWorld

hello3: HelloWorld.c
	$(CC) $(CFLAGS) HelloWorld.c -o HelloWorld
```

Invoke the first target with the following command:

```
make hello -f Makefile2
```

Invoke the second target with the following command:

```
make hello2 -f Makefile2
```

Invoke the third target with the following command:

```
make hello3 -f Makefile2
```

The result of the three preceding targets is the creation of the binary executable `HelloWorld`. However, note that only the rule for `hello3` refers to `$(CC)`, which means that there will be no change if you alter the value of `CC` and run the `hello` target.

In case you’re wondering, one advantage to using macros is that you can replace their definitions in a single location without modifying any of the targets or their dependencies. For example, Listing A.3 defines the `CC` macro with the value of `gcc`; however, you can replace `gcc` with another utility, such as `g++` (if it’s available on your system). Try making this change and execute the same command as above:

```
make hello -f Makefile2
```

The result is the same, which is the creation of the binary executable `HelloWorld`.

There are some standard targets available in makefiles, some of which are shown in the next section.

## A Makefile with Standard Targets

Listing A.4 displays the contents of `Makefile3` that contains three macro definitions and three targets, all of which create the binary executable `HelloWorld`.

### Listing A.4: Makefile3

```
CC=gcc
CFLAGS=-g -Wall
RM=/bin/rm

# only the 'hello' target
all: hello

# just the 'hello' target
hello: HelloWorld.c
	$(CC) $(CFLAGS) HelloWorld.c -o HelloWorld

# what to remove
clean:
	$(RM) HelloWorld
```

Listing A.4 contains only the target `hello`; the targets `hello2` and `hello3` have been removed because they do not serve any useful purpose.

As another illustration, Listing A.5 displays the contents of `Makefile4` that fully “generalizes” the executables that are referenced.

### Listing A.5: Makefile4

```
CC=gcc
CFLAGS=-g -Wall
RM=/bin/rm -f
MAKE=/usr/bin/make
ECHO=echo

# only the 'hello' target
all: hello

# just the 'hello' target
hello: HelloWorld.c
	$(ECHO) "Creating HelloWorld in target hello..."
	$(CC) $(CFLAGS) HelloWorld.c -o HelloWorld

# what to remove
clean:
	$(RM) HelloWorld
```

The initial portion of Listing A.5 contains macros for all the binary executables that are used in the targets, such as `gcc`, `rm`, `make`, and `echo`.
