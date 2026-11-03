# Anatomy of the program:

```
```c
printf("Hello, you are learning C!\\n");
```
```

the library function printf is called with one argument, a character string ending with a \n or new line character.

```
```c
printf("Number of arguments to the main function: %d\n", argc);
```
```

the library function printf is called with two arguments, a character string ending with a \n that includes %d as a placeholder for the second argument argc which is an int.

```
```c
for(i=0; i<argc; i++)
```
```

is a “for loop” in which we do something repeatedly using a counter integer i which is incremented (by the expression i++) at each iteration or looping which continues while i stays less than the value of argc

```
```c
printf("argument number %d is %s\n", i, argv[i]);
```
```

the library function printf is called with three arguments, a character string ending with a \n that includes %d as a placeholder for the second argument argc which is an int, and %s which is a placeholder for the third argument argv[i], the i-th member of the array of pointers to character strings called argv[].

# 1.3  HELLO PROGRAM 3

Lets get real and run this in a web page. Make the extra change adding the first output `printf` statement “Content-type:text/plain\n\n” which tells our server what kind of MIME type is going to be transmitted.

Compile using `gcc -o hello3 chapter1_3.c` and copy the compiled file hello3 to your public_html/cgi-bin directory (or on your own machine as superuser copy the program to /srv/www/cgi-bin (OpenSuse) or /usr/lib/cgi-bin (Ubuntu)).