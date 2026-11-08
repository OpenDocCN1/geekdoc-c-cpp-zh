```
```c
char msg3[15];              //String three to hold the result
//original strings
printf("\nOriginal Messages:\n");
printf("\nMsg1 : %s",msg1);
printf("\nMsg2 : %s",msg2);
//copy string
strcpy(msg3,msg2);
printf("\n\nMessages after copying:\n");
printf("\nMsg1 : %s",msg1);
printf("\nMsg2 : %s",msg2);
printf("\nMsg3 : %s",msg3);
printf("\n\nLength of Messages before concatenation:\n");
printf("\nMsg1 : %d", strlen(msg1));
printf("\nMsg2 : %d", strlen(msg2));
//string concatenation
strcat(msg1,msg2);
printf("\n\nMessages after concatenation:\n");
printf("\nMsg1 : %s",msg1);
printf("\nMsg2 : %s",msg2);
printf("\n\nLength of Messages after concatenation:\n");
printf("\nMsg1 : %d", strlen(msg1));
printf("\nMsg2 : %d", strlen(msg2));
getch();
}
```
```

# Output:

Original Message
Msg1 : Good
Msg2 : Morning

Messages after copying
Msg1 : Good
Msg2 : Morning
Msg3 : Morning

Length of Messages before concatenation
Msg1 : 4
Msg2 : 7