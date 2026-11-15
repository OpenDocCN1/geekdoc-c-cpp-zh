
![](img/02c4582f051c5b51776411c92b079035_119_0.png)

Although the default clause in the switch statement is optional, we recommend that it be included so that the steps are clearly specified for the situation in which none of the case labels is equal to the controlling expression. We also use the break statement in the default clause to emphasize that the program continues with the statement following the switch statement.

It is valid to use several case labels with the same statement, as in the following:

```
switch (op_code)
{
    case 'N': case 'R':
        printf("Normal operating range \n");
        break;
    case 'M':
        printf("Maintenance needed \n");
        break;
    default:
        printf("Error in code value \n");
        break;
}
```

When more than one case label is used for the same statement, the evaluation is performed as if the logical operator || joined the cases. For this example, the first statement is executed if op_code is equal to 'N' or if op_code is equal to 'R'.

## PRACTICE!

Convert the following nested if/else statements to a switch statement:

```
if (rank==1 || rank==2)
    printf("Lower division \n");
else
{
    if (rank==3 || rank==4)
        printf("Upper division \n");
    else
    {
        if (rank==5)
            printf("Graduate student \n");
        else
            printf("Invalid rank \n");
    }
}
```

## 3.4 Problem Solving Applied: Face Recognition

In this section, we use the new statements presented in this chapter to solve a problem related to facial recognition.

One technique for comparing faces uses ratios of distances between key points on a face, as indicated in Figure 3.7. These ratios might include the distance between the eyes divided by the distance between the nose and the chin. Because these measurements are ratios, they

![](img/02c4582f051c5b51776411c92b079035_120_0.png)

Figure 3.7 Key points for face recognition.

can be computed from images of different sizes and should still be similar for the same face. The computer programs that compute these measurements must be able to locate a face in an image and then also locate the eyes and other key points on the face. There are additional challenges if the head is turned in a different direction in one of the images.

For this problem, assume that we have three images of a person looking at the camera. We would like to determine if the two images are likely to be the same person. The technique that we will use is one that compares ratios of the distances between the outer edges of the eyes to the distances between the tip of the chin and the tip of the nose. Write a C program to read the two distances for each face, compute the ratios, and then determine which two images have the closest ratios.

### 1. PROBLEM STATEMENT

Given information on three faces, use ratios to determine the two faces that are the most similar.

### 2. INPUT/OUTPUT DESCRIPTION

The following diagram shows that the inputs to the program are the distance between the outer edges of the eyes and the distance between the tip of the chin and the tip of the nose, for three different images. The output is the image numbers for the two images that are most similar based on ratios of these distances.

![](img/02c4582f051c5b51776411c92b079035_120_1.png)

### 3. HAND EXAMPLE

Assume that the following distances are measured from the three images, in cm:

| | Image 1 | Image 2 | Image 3 |
|---|---|---|---|
| Outer eye distance | 5.7 | 6.0 | 6.0 |
| Nose to chin distance | 5.3 | 5.0 | 5.6 |

We can then compute the ratio of the outer eye distance to the nose to chin distance for each image:

```
ratio_1 = 5.7/5.3 = 1.08
ratio_2 = 6.0/5.0 = 1.20
ratio_3 = 6.0/5.6 = 1.07
```

We then compute the differences between each pair of ratios, using an absolute value so that each difference is a positive number:

```
diff_1_2 = |ratio_1 - ratio_2| = |1.08 - 1.20| = 0.12
diff_1_3 = |ratio_1 - ratio_3| = |1.08 - 1.07| = 0.01
diff_2_3 = |ratio_2 - ratio_3| = |1.20 - 1.07| = 0.13
```

The difference with the smallest value then determines the two images that are the most similar, using these two distances. In this case, image 1 and image 3 are the closest. Note that it is possible that all these differences are large, and thus the smallest of the three may still not represent a good match. Commercial face recognition systems that use distances use a large number of distances in order to improve their accuracy.

### 4. ALGORITHM DEVELOPMENT

The first step in the development of an algorithm is the decomposition of the problem solution into a set of sequentially executed steps.

### Decomposition Outline

- 1. Read the distances for each image.
- 2. Compute the ratios for each image.
- 3. Compute the differences between each pair of ratios.
- 4. Find the minimum difference.
- 5. Print the corresponding image numbers as the best match.

This program has a simple structure, so we can convert the decomposition directly into C.

```
//* ---------------------------------------------------------- */
//* Program chapter3_1 */
//* */
//* This program selects the two images that are most similar */
//* using the distance between the eyes and the distance */
//* between the nose and the chin.
```

```
#include <stdio.h>
#include <math.h>

int main(void)
{
    /* Declare variables. */
    double eyes_1, eyes_2, eyes_3, nose_chin_1, nose_chin_2,
           nose_chin_3, ratio_1, ratio_2, ratio_3, diff_1_2,
           diff_2_3, diff_1_3;

    /* Get user input from the keyboard. */
    printf("Enter values in cm. \n");
    printf("Enter eye distance and nose-chin distance for image 1: \n");
    scanf("%lf %lf", &eyes_1, &nose_chin_1);
    printf("Enter eye distance and nose-chin distance for image 2: \n");
    scanf("%lf %lf", &eyes_2, &nose_chin_2);
    printf("Enter eye distance and nose-chin distance for image 3: \n");
    scanf("%lf %lf", &eyes_3, &nose_chin_3);

    /* Compute ratios. */
    ratio_1 = eyes_1 / nose_chin_1;
    ratio_2 = eyes_2 / nose_chin_2;
    ratio_3 = eyes_3 / nose_chin_3;

    /* Compute differences. */
    diff_1_2 = fabs(ratio_1 - ratio_2);
    diff_1_3 = fabs(ratio_1 - ratio_3);
    diff_2_3 = fabs(ratio_2 - ratio_3);

    /* Find minimum difference and print image numbers. */
    if ((diff_1_2 <= diff_1_3) && (diff_1_2 <= diff_2_3))
        printf("Best match is between images 1 and 2 \n");
    if ((diff_1_3 < diff_1_2) && (diff_1_3 <= diff_2_3))
        printf("Best match is between images 1 and 3 \n");
    if ((diff_2_3 < diff_1_3) && (diff_2_3 < diff_1_2))
        printf("Best match is between images 2 and 3 \n");

    /* Exit program. */
    return 0;
}
/*--------------------------------------------------------------*/
```

### 5. TESTING

We first test the program with the data from the hand example. This generates the following interaction:

```
Enter values in cm.
Enter eye distance and nose-chin distance for image 1:
5.7 5.3
Enter eye distance and nose-chin distance for image 2:
6.0 5.0
Enter eye distance and nose-chin distance for image 3:
6.0 5.6
Best match is between images 1 and 3
```

The answer matches the hand example, so we can then test the program with additional lengths. Print an image of each of three different friends and see if you can predict which pair would be the best match for this very simple face recognition system. Run the program with information from two different images of the same person and a third person to see if this technique selects the two images that are from the same person.

### MODIFY!

These problems relate to the program developed in this section for finding the best matching pair from three images.

- 1. Modify the program so that it also prints out all three differences. This gives additional information about the quality of the match; if the differences are small, the quality of the match is better.
- 2. What would the output be if two of the ratios were the same minimum value? What would the output be if all three of the ratios were the same value? Generate data to make these cases happen and check your answers.
- 3. Modify the program to use a nested if statement in the solution instead of three independent if statements. Does the answer to Problem 2 change with this solution?
- 4. Modify the program to print the image numbers for the two images that are the most different.
- 5. Modify the program to print the best match between four images. (Note that this causes the program to get longer, because with four images there are six possibilities. In Chapter 5 we will learn additional C language functionality that allows us to handle situations such as this one without ever increasing lines of code.)

## 3.5 Loop Structures

Loops are used to implement repetitive structures. C contains three different loop structures—the while loop, the do/while loop, and the for loop. In addition, C allows us to use two additional statements with loops to modify their performance—the break statement (which we used with the switch statement) and the continue statement.
