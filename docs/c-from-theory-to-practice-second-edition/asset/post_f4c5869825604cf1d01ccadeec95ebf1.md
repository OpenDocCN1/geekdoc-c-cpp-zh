
## 20

## Review Exercises

### C.20.1 Write a program that reads its command line arguments and allocates memory to concatenate them into one string and display that string.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int main(int argc, char *argv[])
{
    char *tot_str;
    int i, tot_chars;
    if(argc == 1) /* Check if the command line contains only the name of the program. */
    {
        printf("Missing arguments ...\n");
        exit(EXIT_FAILURE);
    }
    tot_chars = 0; /* It counts the characters of all arguments. */
    for(i = 1; i < argc; i++) /* Remember that argv[1] points to the first argument, argv[2] to the second one, and so on. argv[0] points to the name of the program. */
        tot_chars += strlen(argv[i]);
    tot_str = (char*) malloc(tot_chars+1); /* Allocate an extra place for the null character. */
    if(tot_str == NULL)
    {
        printf("Error: Not available memory\n");
        exit(EXIT_FAILURE);
    }
    *tot_str = '\0'; /* Store the null character. */
    for(i = 1; i < argc; i++)
        strcat(tot_str, argv[i]);
    printf("The merged string is: %s\n", tot_str);
    free(tot_str);
    return 0;
}
```

### C.20.2 What is the output of the following program?

```c
#include <stdio.h>
void test(int **tmp, int i);
int main(void)
{
    int **tmp, *ptr, i, arr[] = {10, 20, 30};
    ptr = arr;
    tmp = &ptr;
    for(i = 0; i < 3; i++)
    {
        test(tmp, i);
        printf("%d ", arr[i]);
    }
    return 0;
}
```

```c
void test(int **tmp, int i)
{
    *(*(tmp + i)) += 50;
}
```

Answer: tmp is declared as a pointer to a pointer to an integer. The statement tmp = &ptr; makes tmp point to the address of ptr; which points to the address of the first element of the array arr. Since *tmp is equal to ptr, we have *(tmp+i) = *(ptr+i) = *(arr+i) = arr[i]. Therefore, each call to test() increases the respective element of the array arr by 50, and the program displays: 60 70 80.

### C.20.3 Write a program that reads the order of preference that 100 tourists answered in the question: “What did you enjoy the most in Greece?”

- 1. The natural diversity
- 2. The climate
- 3. The islands
- 4. The night life
- 5. The monuments
- 6. The people
- 7. The food

Each answer takes 1–7 points according to its rank order. The first answer takes 7 points, the second one takes 6 points, and the last one takes 1 point. For example, if two tourists answered the following:

| First Tourist | Second Tourist |
|---|---|
| 5 (7p.) | 3 (7p.) |
| 4 (6p.) | 7 (6p.) |
| 6 (5p.) | 2 (5p.) |
| 3 (4p.) | 1 (4p.) |
| 2 (3p.) | 5 (3p.) |
| 1 (2p.) | 4 (2p.) |
| 7 (1p.) | 6 (1p.) |

the program should display:

First answer gets 6 points
Second answer gets 8 points

Third answer gets 11 points
Fourth answer gets 8 points
Fifth answer gets 10 points
Sixth answer gets 6 points
Seventh answer gets 7 points

The program should read valid answers in [1,7] and check if the answer is already given. If it is, the program should display a message and prompt the user to enter a new one.

```c
#include <stdio.h>
#include <string.h>

#define TOURISTS 100
#define ANSWERS 7

int main(void)
{
    int i, j, sel, pnts[ANSWERS] = {0}; /* This array holds the points of each answer. For example, pnts[0] holds the points of the first answer, pnts[1] holds the points of the second answer and so on. */
    int given_ans[ANSWERS] = {0}; /* This array is used to check whether an answer is already given or not. If an element's value is 1, it means that the respective answer is chosen. For example, if the user chooses the third answer, given_ans[2] becomes 1. */
    for(i = 0; i < TOURISTS; i++)
    {
        printf("\nEnter answers of tourist_%d:\n", i+1);
        memset(given_ans, 0, sizeof(given_ans)); /* The values must be zeroed before reading the answers of a new tourist. See memset() in Appendix C. */
        for(j = 0; j < ANSWERS; j++)
        {
            while(1) /* Infinite loop until the user enters a valid answer, not already given. */
            {
                printf("Answer_%d [1-%d]: ", j+1, ANSWERS);
                scanf("%d", &sel);
                if(sel < 1 || sel > ANSWERS)
                    printf("Wrong answer ...\n");
                else if(given_ans[sel-1] == 1)
                    printf("Error: This answer is already given ...\n");
                else
                    break;
            }
            pnts[sel-1] += ANSWERS - j; /* For example, if the first answer (j = 0) is the first one, then pnts[sel-1] - pnts[5-1] - pnts[4] += 7-0 = 7; that is, 7 more points are added to the points of the fifth choice. */
            given_ans[sel-1] = 1;
        }
    }
    printf("\n***** Answer Results *****\n");
    for(i = 0; i < ANSWERS; i++)
        printf("Answer_%d gets %d points\n", i+1, pnts[i]);
    return 0;
}
```

### C.20.4
Write a program that requires two command line arguments that correspond to the dimensions (rows and columns) of a two-dimensional array of doubles. The program should allocate memory to create the array and assign random values to its elements so that the sum of the elements in each row is equal to 1. The program should display the elements of the array before it terminates.

NOTE: To convert the command line arguments to integers, use the atoi() function. See its prototype in Appendix C.

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main(int argc, char *argv[])
{
    int i, j, rows, cols;
    double **arr, sum_line;

    if(argc < 3)
        printf("Error: missing arguments...\n");
    else if(argc == 3)
    {
        rows = atoi(argv[1]); /* Convert the second argument to integer. */
        cols = atoi(argv[2]); /* Do the same for the third argument. */
        srand(time(NULL));
        arr = (double**) malloc(rows * sizeof(double*));
        if(arr == NULL)
        {
            printf("Error: Not available memory\n");
            exit(EXIT_FAILURE);
        }
        for(j = 0; j < rows; j++)
        {
            arr[j] = (double*) malloc(cols * sizeof(double));
            if(arr[j] == NULL)
            {
                printf("Error: Not available memory\n");
                exit(EXIT_FAILURE);
            }
        }
        for(i = 0; i < rows; i++)
        {
            sum_line = 0;
            for(j = 0; j < cols-1; j++)
            {
                arr[i][j] = (rand()%101/(cols-1))/100.0;
                sum_line += arr[i][j]; /* As an example, assume that the number of columns is 5. For the first four rows' elements rand()%101 generates an integer in [0, 100]. Dividing it by the number of the columns minus 1, that is, 4, we get an integer in [0, 25] and dividing that integer with 100.0 we get a number in [0, 0.25]. In this way, the sum of the first four elements is constrained in [0, 1]. */
            }
            arr[i][j] = 1-sum_line; /* To satisfy the requirement that the sum of the elements of each row must be equal to 1, the value of the last element is calculated by subtracting from 1 the sum of the remaining elements. */
        }
        for(i = 0; i < rows; i++)
        {
            for(j = 0; j < cols; j++)
                printf("%6.2f", arr[i][j]);
            printf("\n");
        }
        for(j = 0; j < rows; j++)
            free(arr[j]);
        free(arr);
    }
    else
        printf("Error: too many arguments...\n");
    return 0;
}
```

### C.20.5 For a system to connect to an Internet address, its network card must transmit an Internet Protocol (IP) packet that encapsulates a special TCP segment. The IPv4 header format is depicted in Figure 20.1.

![](img/b8da5dcf9ba7f1fad5213c453d095246_655_0.png)

FIGURE 20.1
IPv4 header.

![](img/b8da5dcf9ba7f1fad5213c453d095246_656_0.png)

FIGURE 20.2
TCP header.

The TCP header format is depicted in Figure 20.2.

Write a program that reads the source IP address in x.x.x.x format (each x is an integer in [0, 255]), the destination IP address in x.x.x.x format, and the TCP destination port (integer in [1, 65535]) and creates an IP packet that encapsulates the proper TCP segment. The program must store the content of the IP packet in hexadecimal format in a user-selected text file. Each line must contain 16 bytes. Set the following values in the IPv4 header:

- a. Version = 4.
- b. IHL = 5.
- c. Total Length = total length of the IP packet, including the TCP data.
- d. Protocol = 6.
- e. Time to Live = 255.
- f. Destination Address = destination IP address.
- g. Source Address = source IP address.

Set the following values in the TCP header:

- a. Destination Port = destination TCP port.
- b. Source Port = 1500.
- c. Window = the maximum allowed value.
- d. SYN bit = 1.

Set the remaining fields to 0 and assume that there are no Options fields.

The program has one restriction; if the destination IP address starts from 130.140 or 160.170 and the TCP destination port is 80, do not create the IP packet and display a related message.

```c
#include <stdio.h>
#include <stdlib.h>

typedef unsigned char BYTE;
```
