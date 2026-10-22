Let’s tackle a particular case of representing data. Suppose you want to write a program that enables you to enter a list of all the movies (including videotapes, DVDs, and Blu-ray) you’ve seen in a year. For each movie, you’d like to record a variety of information, such as the title, the year it was released, the director, the lead actors, the length, the kind of film (comedy, science fiction, romance, drivel, and so forth), your evaluation, and so on. That suggests using a structure for each film and an array of structures for the list. To simplify matters, let’s limit the structure to two members: the film title and your evaluation, a ranking on a 0-to-10 scale. Listing 17.1 shows a bare-bones implementation using this approach.

```
Listing 17.1  **The `films1.c` Program**

```c
/* films1.c -- using an array of structures */
#include <stdio.h>
#include <string.h>
#define TSIZE          45      /* size of array to hold title  */
#define FMAX           5       /* maximum number of film titles */

struct film {
    char title[TSIZE];
    int rating;
};
char * s_gets(char * st, int n);
int main(void)
{
    struct film movies[FMAX];
    int i = 0;
    int j;

    puts("Enter first movie title:");
    while (i < FMAX && s_gets(movies[i].title, TSIZE) != NULL &&
           movies[i].title[0] != '\0')
    {
        puts("Enter your rating <0-10>:");
        scanf("%d", &movies[i++].rating);
        while (getchar() != '\n')
            continue;
        puts("Enter next movie title (empty line to stop):");
    }
    if (i == 0)
        printf("No data entered. ");
    else
        printf ("Here is the movie list:\n");

        for (j = 0; j < i; j++)
            printf("Movie: %s Rating: %d\n", movies[j].title,
                   movies[j].rating);
}
```
```