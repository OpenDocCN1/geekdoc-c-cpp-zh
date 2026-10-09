# Figure 35.1 Pointers on the stack to a buffer of floats

![](bbox=[0.2, 0.145, 0.815, 0.275])

**malloc**() allocates a buffer on the heap, so you need to make sure that you free it when you are done. Wouldn’t it be great if you could declare that buffer as part of the frame (on the stack) so that it would be deallocated automatically when the function is done executing? You can. Change **main.c**:

```
```
import <stdio.h>

float averageFloats(float *data, int dataCount)
{
    float sum = 0.0;
    for (int i = 0; i < dataCount; i++) {
        sum = sum + data[i];
    }
    return sum / dataCount;
}

int main (int argc, const char * argv[]) {
    
    // Declares the array as part of the frame
    float gradeBook[3];
    
    gradeBook[0] = 60.2;
    gradeBook[1] = 94.5;
    gradeBook[2] = 81.1;
    
    // Calculate the average
    float average = averageFloats(gradeBook, 3);
    
    // No need to free the array!
    // Cleanup happens automatically when the function returns
    
    printf("Average = %.2f\n", average);
    
    return 0;
}
```
```

Build and run it.

The string literal made it easy to pack an array with characters. There are also array literals. Use one to initialize *gradeBook*: