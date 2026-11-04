```
printf("Enter last name: ");
fgets(last, sizeof(last), stdin);

strcpy(full, first);
strcat(full, " ");
strcat(full, last);

printf("The name is %s\n", full);

return (0);
}
```

Listing 2.22 declares the character variables first, last, and fullName of lengths 100, 100, and 200, respectively. Next, the main() function uses 2 different printf() statements that prompts users for a first name and last name, using the built-in gets() C function to capture those input values.

The next part of the code uses the built-in strcpy() C function to copy first to the variable full. Next, the built-in strcat() function appends a space (" "), and then appends last to the variable full. A sample invocation of launching the code in Listing 2.22 is here:

Enter first name: john
Enter last name: smith
The name is john
smith

Notice that the full name is displayed on separate lines, which happens because users must press a <RETURN> after entering the first name, and the <RETURN> character is included in the variable full. We can remove the <RETURN> character simply by uncommenting the following code snippet:

```
first[strlen(first)-1] = '\0';
```