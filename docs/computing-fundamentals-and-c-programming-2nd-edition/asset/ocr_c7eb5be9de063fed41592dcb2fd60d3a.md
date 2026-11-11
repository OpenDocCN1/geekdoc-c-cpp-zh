```
Program

struct class
{
    int number;
    char name[20];
    float marks;
};

main()
{
    int x;
    struct class student1 = {111,"Rao",72.50};
    struct class student2 = {222,"Reddy", 67.00};
    struct class student3;

    student3 = student2;

    x = ((student3.number == student2.number) &&
         (student3.marks == student2.marks)) ? 1 : 0;

    if(x == 1)
    {
        printf("\nstudent2 and student3 are same\n\n");
        printf("%d %s %f\n", student3.number,
               student3.name,
               student3.marks);
    }
    else
        printf("\nstudent2 and student3 are different\n\n");

}

Output

student2 and student3 are same

222 Reddy 67.000000
```

**Fig. 12.2** Comparing and copying structure variables

# 12.5.1 Word Boundaries and Slack Bytes

Computer stores structures using the concept of “word boundary”. The size of a word boundary is machine dependent. In a computer with two bytes word boundary, the members of a structure are stored left_aligned on the word boundary, as shown below. A character data takes one byte and an integer takes two bytes. One byte between them is left unoccupied. This unoccupied byte is known as the *slack byte*.