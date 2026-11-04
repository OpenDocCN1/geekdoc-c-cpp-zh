# TABLE 5.1
Weight Categories

| Mass Index | Result |
|---|---|
| BMI < 20 | Lower than normal weight |
| 20 <= BMI <= 25 | Normal weight |
| 25 < BMI <= 30 | Overweight |
| 30 < BMI <= 40 | Obese |
| 40 < BMI | Extremely obese |

C.5.7 Write a program that reads a man's height (in meters) and weight (in kilograms) and calculates his body mass index (BMI) using the formula BMI = weight/height². The program should display the BMI and a corresponding message according to Table 5.1, and the lower and upper limit of the normal weight for the given height.

```
~~~c
#include <stdio.h>
int main(void)
{
    float bmi, height, weight;

    printf("Enter height (in meters): ");
    scanf("%f", &height);

    printf("Enter weight (in kgrs): ");
    scanf("%f", &weight);

    bmi = weight/(height*height);
    printf("***** BMI: %.2f\n", bmi);

    if(bmi < 20)
        printf("Under normal weight\n");
    else if(bmi <= 25) /* Since the previous if checks values up to
20, this condition is equivalent to: else if (bmi >= 20 && bmi <= 25). */
        printf("Normal weight\n");
    else if(bmi <= 30)
        printf("Overweight\n");
    else if(bmi <= 40)
        printf("Obese\n");
    else
        printf("Serious obesity\n");

    printf("According to your height the bounds of normal weight are [%.2f-%.2f]\n", 20*height*height, 25*height*height); /* The lower and the
upper bmi limits for normal weight are 20 and 25, respectively. */
    return 0;
}
~~~
```

C.5.8 To change the PIN code of a mobile phone, the user is asked to enter the current PIN code and the device checks if that code is equal to the one stored in the SIM card. If they are the same, the user is asked to enter the new PIN code once more for verification, and if it is entered correctly, it is stored in the SIM card. Write a program that simulates this process. Assume that the current code stored in SIM is 1234.