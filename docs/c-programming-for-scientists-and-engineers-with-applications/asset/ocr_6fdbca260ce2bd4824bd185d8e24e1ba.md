```
/* height - height the projectile reaches */
/* Output Variables: */
/* initvel - initial velocity of firing ft/sec* */
/* height - height the projectile reaches */
/****************************************************************
```

```
#include <stdio.h>

int main() {
    const float GRAV_ACCEL = 32.2;
    float initvel,height;

    printf("Initial Velocity \tHeight\n\n");
    initvel = 50;
    while(initvel <= 200) {
        height = - (initvel * initvel) / (2.0 * GRAV_ACCEL);
        printf("%6.2f\t%8.2f\n", initvel, -1.0 * height);
        initvel += 50;
    }
    return 0;
}
```

Output

Initial Velocity \tHeight
50.00\t38.82
100.00\t155.28
150.00\t349.38
200.00\t621.12