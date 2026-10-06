
## Objective-C 分数类

现在是时候在 Objective-C 中定义一个实际类并学习如何处理该类的实例了。再次，你将首先学习。假设你需要编写一个处理分数的程序。你可能需要处理加法、乘法等。如果你不知道类，你可能会从一个这样的简单程序开始：

程序 3.1

处理分数的简单程序

```
#import <Foundation.h>

int main (int argc, char * argv[]) {
  @autoreleasepool {
    int numerator = 1;
    int denominator = 3;
    NSLog("The fraction is %i/%i", numerator, denominator);
  }
}
```

程序 3.1 输出

The fraction is 1/3
