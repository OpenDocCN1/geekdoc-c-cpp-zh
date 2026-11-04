Chapter 6. Another point to keep in mind is that the following format is valid in some operating systems:

```
int main(int argc, char **argv, char **envp)
```

The fourth code snippet contains a third parameter envp that “points” to the environment (i.e., the environment variables) where a C program is launched. However, you can access and update environment variables via getenv() and putenv(), respectively, which are discussed in Chapter 6.

If you want to specify command line arguments that are accessible inside a C program, you need to use the following syntax (which is a commonly used syntax):

```
int main(int argc, char **argv)
```

The first argument argc is a number that equals the number of command line arguments. The second argument argv in the preceding snippet is a pointer-to-a-pointer, which we’ll see in a later chapter. Note that you can use the preceding syntax in Listing 1.1 and the code compilation is performed in the same manner.

# C Program Syntax

There are several conventions for placing curly braces in C programs, and the comments in this section are generally applicable to code blocks in C. We’ll use the code in Listing 1.1 as a simple illustration for program syntax. Depending on your preference, you can place the initial curly brace in Listing 1.1 on the same line, as shown here:

```
int main() {
    printf("Hello World\n");
}
```