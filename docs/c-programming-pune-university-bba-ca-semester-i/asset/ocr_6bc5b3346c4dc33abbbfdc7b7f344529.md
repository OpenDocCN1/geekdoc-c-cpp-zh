+   3.
+   ```c
+   #include<string.h>
+   #include<ctype.h>
+   int main(void)
+   {
+       int length,i;
+       char string[ ] = "This is A string";
+       length = strlen(string);
+       for (i=0, i<length; i++)
+       {
+           string[i]=to_lower(string[i]);
+       }
+       printf("%s\n",string);
+       getch();
+       return 0;
+   }
+   ```

# Winter 2016

+   1. Define string with example.

+   2. What is an Array? Give an example.

+   3.
+   ```c
+   main()
+   {
+       char string[ ] = "HELLO WORLD";
+       int m;
+       for (m=0;string[m] !='\0'; m++)
+       if((m % 2 ) ==0)
+       printf("%c", string [m]);
+   }
+   ```

+   4.
+   ```c
+   main()
+   {
+       int c,d;
+       char string[ ] ="A B C D";
+       printf("\n\n");
+       for(c=0;c<11;c++)
+       {
+           d=c=1;
+           printf("%-12.*s\n",d,string);
+       }
+       printf("\n");
+   ```
+