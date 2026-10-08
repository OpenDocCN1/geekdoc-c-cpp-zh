
typedef struct contact Contact;
/* Declaration of structure variables */
Contact contact1, contact2;
/* Initialize structure members of contact1 */
printf("Enter the information of contact 1:\n");
scanf("%[^\n]",contact1.c_name);
printf("\n Enter Phone number: ");
scanf("%ld",&contact1.li_phoneno);
printf("\n Enter e-mail address: ");
scanf(" %s",contact1.c_email);

/* Initialize structure members of contact2 */
printf("\nEnter the information of contact 2:\n");
scanf("\n Enter name: ");
scanf(" %[^\n]", contact2.c_name);
printf("\n Enter Phone number: ");
scanf("%ld",&contact2.li_phoneno);
printf("\n Enter e-mail address: ");
scanf(" %s", contact2.c_email);

/* Display structure members of contact1 */
printf("\nHere is the information of contacts recently entered...");
printf("\nInformation of Contact 1\n");
printf("  Name : %s\n",contact1.c_name); /* Displaying structure
member value */
printf("  Phone Number : %ld\n", contact1.li_phoneno);
printf("  Email address : %s\n", contact1.c_email);

printf("\nInformation of Contact 2\n");
printf("  Name : %s\n",contact2.c_name);
printf("  Phone Number : %ld\n", contact2.li_phoneno);
printf("  Email address : %s\n", contact2.c_email);
return;
}
/* End of function main */

# Output:

Enter the information of contact 1:
Enter name: Harshit Jain
Enter Phone number: 2341234
Enter e-mail address: harshitjain123@rediffmail.com

Enter the information:
Enter name: Vidita Arolikar
Enter Phone number: 30063450
Enter e-mail address: vidital23_aroikar@yahoo.com
Here is the information of contacts recently entered...

Information of Contact 1
Name : Harshit Jain
Phone Number : 2341234
Email address : harshitjain123@reddiffmail.com

Information of Contact 2
Name : Vidita Aroldar
Phone Number : 30063450
Email address : vidita123_arolokar@yahoo.com

It can be seen in Program 2 that we have used statements such as `scanf("%[^\n]",contact1.c_name)`, `scanf("%ld", &contact1.li_phono)`, and `scanf("%s", contact1.c_email)` to accept the values from the user.

The usage of the scan function is similar to that of normal variable, except for the difference in the variable name. Figure 6 shows this difference:

![](img/5d422ba7108ffdf64376be51eaf0c459_239_0.png)

In Figure 6, `contact1` refers to the variable of type structure and `c_name` is the data member defined in the template. To associate them, we put a dot in between the two. Thus, two data elements can now be easily differentiated, for example, `contact1.c_email` and `contact2.c_email` refers to two totally different data elements. The first data element refers to the email of `contact1`, while the second data element refers to the email of `contact2`.

In Program 2, we asked the user to enter the values of structure data members through keyboard. It is also possible to predefine these values. The next section discusses how to predefine structure data member value.

### 11.6 Initializing Structure Members

Similar to other variables, the structures variables can be initialized at the time of declaration. Program 3 illustrates structure variable initialization at compile time:

**▶ Program 3**

/* Program to initialize a new contact at declaration time */

#include<stdio.h>
/* Beginning of main function */
main()
{
/* Declaration of structure */
struct contact
{
    char c_name[25];
    char c_email[30];
    unsigned long int li_phoneno;
};
/* Structure alias */
typedef struct contact Contact;

/* Initialize structure variables at declaration time */
Contact contact1= {"Harshit Jain","harshitjain123@rediffmail.com",2341234};

/* Print the structure data elements */
printf("\nInformation of contact 1....\n");
printf(" Name : %s\n",contact1.c_name);
printf("  Phone Number : %ld\n", contact1.li_phoneno);
printf("  Email address : %s\n", contact1.c_email);
return;
}
/* End of function main */

**Output:**

Information of contact 1
  Name : Harshit Jain
  Phone Number: 2341234
  Email address: harshitjain123@rediffmail.com

In Program 3, the data members can be assigned values at the time of definition of a structure variable. As a structure is used as a data type in C language, we can assign the value of one structure to another. The syntax for assignment of structure is as follows:

```
structure variable 1 = structure variable 2;
```

However, to perform assignment operation, both the structure variables should be of the same data type. Program 4 illustrates how to copy values of all the data members of the structure variable `contact1` into `contact2`:

**▶ Program 4**

/* Program to copy structure variables */

#include<stdio.h>

/* Beginning of main function */
main()
{
/* Declaration of structure */
struct contact
{
    char c_name[25];
    char c_email[30];
    unsigned long int li_phoneno;
};

/* Structure alias */
typedef struct contact Contact;
/* Initialize structure variables at declaration time */
Contact contact1= {"Harshit Jain","harshitjain123@rediffmail.com",2341234};
/* Assign value of contact 1 to contact 2 */
Contact contact2=contact1;
/* Print the structure data elements */
printf("Details of contact1....\n");
printf(" Name : %s\n",contact1.c_name);
printf(" Phone Number : %ld\n", contact1.li_phoneno);
printf(" Email address : %s\n", contact1.c_email);
printf("Details of contact2....\n");
printf(" Name : %s\n",contact2.c_name);
printf(" Phone Number : %ld\n", contact2.li_phoneno);
printf(" Email address : %s\n", contact2.c_email);
return;
}
/* End of function main */

**Output:**

Details of contact1....
Name: Harshit Jain
Phone Number: 2341234
Email address: harshitjain123@rediffmail.com
Details of contact2....
Name: Harshit Jain
Phone Number: 2341234
Email address: harshitjain123@rediffmail.com

It can be seen in Program 4 that the output data of all the data elements of contact 1 are copied into the data elements of contact 2. In all the programs discussed earlier, the data types of structure data members were primitive. It is also possible to use derived data type along with structure data type. For example, we can define data members that can be of structure type. A structure in which other structure is defined as the data member is known as nested structure. The next section discusses about the nested structure in detail.

### 11.7 Nested Structure

We have already seen that a structure can hold data members of different primitive data types such as integer, character, float, and double as well as derived data type like array. It is interesting to note that the structures can also hold data members that are of structure data type. The structure that is required to be used as a data member must be declared before the structure that it is to be used in.

Assume that we need to store the birth date of each contact used in the programs made till now. We know that the birth date is composed of three components, namely, date, month, and year. At times, calculations are to be performed on the individual components of the birth date. For example, to calculate the age of a person, difference of current date and birth date is done. Thus, it is advisable to store date, month, and year in separate variables. Storing them in different variables and holding them as a group in a structure will make its use easier. Program 5 illustrates the use of nested structure:

# Program 5

/* Program to illustrate structure within structure*/
#include<stdio.h>

/* Beginning of main function */
main()
{
   /* Declaration of structures */
   struct date
   {
       unsigned int i_dd;
       unsigned int i_mm;
       unsigned int i_yyyy;
   };

   struct contact
   {
       char c_name[25];
       char c_email[30];
       unsigned long int li_phoneno;
       struct date dob;
       /* Structure variable defined within structure*/
   };

   typedef struct contact Contact;
   Contact contact1;
   /* Initialize structure members of contact1 */
   printf("\n Enter the information:\n");
   printf("\n Enter name: ");
   scanf(" %[\n]", contact1.c_name);
   printf("\n Enter Phone number: ");
   scanf("%ld", &contact1.li_phoneno);
   printf("\n Enter e-mail address : ");
   scanf(" %s", &contact1.c_email);
   printf("\n Enter Birthdate (dd mm yyyy) : ");
   scanf("%u %u %u", &contact1.dob.i_dd, &contact1.dob.i_mm,
   &contact1.dob.i_yyyy);

   /* Print the structure data elements */
   printf("\nThe information of contacts recently entered....\n");
   printf(" Name : %s\n\n", contact1.c_name);
   printf(" Phone Number : %ld\n\n", contact1.li_phoneno);
   printf(" Email address : %s\n\n", contact1.c_email);
   printf(" Birthdate : ");
   printf("%u-%u-%u\n\n", contact1.dob.i_dd, contact1.dob.i_mm,
   contact1.dob.i_yyyy);
   return;
}
/* End of function main */

**Output:**

Enter the information:
