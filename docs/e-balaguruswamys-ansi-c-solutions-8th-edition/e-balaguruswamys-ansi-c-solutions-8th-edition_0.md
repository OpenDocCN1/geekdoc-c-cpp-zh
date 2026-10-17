
# E. Balaguruswamy 的 ANSI C 解决方案：第 8 版

## 2.1

```c
#include <stdio.h>
int main(){
  int a=5,b=8,c=18;
  printf("%dx + %dy = %d",a,b,c);
  return 0;
}
```

## 2.2

```c
/* void bar3d(int left, int top, int right, int bottom, int depth, int topflag);
其中，left 指定左上角的 X 坐标，top 指定左上角的 Y 坐标，right 指定右下角的 X 坐标，bottom 指定右下角的 Y 坐标，depth 指定条形以像素为单位的深度，topflag 决定是否在条形上放置一个三维顶端（如果为非零则放置，否则不放置） */
#include <graphics.h>
int main(){
  /* gm 是图形模式（Graphics mode），这是一种使用像素生成图像的计算机显示模式。DETECT 是在"graphics.h" 头文件中定义的宏宏 */
  int gd = DETECT, gm;
  // initgraph 通过从磁盘加载图形驱动程序初始化图形系统
  initgraph(&gd, &gm, "");
  // 侧边位置
  int left, top, right, bottom;
  // 条形的深度
  int depth;
  // topflag 表示顶线。
  int topflag;
  // left, top, right, bottom, depth, topflag 的位置
  bar3d(left = 150, top = 250, right = 190, bottom = 350, depth = 20, topflag = 1);
  bar3d(left = 220, top = 150, right = 260, bottom = 350, depth = 20, topflag = 0);
  bar3d(left = 290, top = 200, right = 330, bottom = 350, depth = 20, topflag = 1);
  // y 轴线
  line(100, 50, 100, 350);
  // x 轴线
  line(100, 350, 400, 350);
  getch();
  // closegraph 函数关闭图形模式并释放图形系统分配的所有内存。
  closegraph();
  return 0;
}
```

## 2.3

```c
#include <stdio.h>
int main(){
  for(int i=1;i<=10;i++)
    printf("5 x %d = %d\n",i,(5*i));
  return 0;
}
```

## 2.4

```c
#include <stdio.h>
int main(){
  int a,b,c;
  float x=a/(b-c);
  printf("\n x = %f ");
  return 0;
}
```

## 2.5

```c
#include <stdio.h>
int main(){
  printf("请输入行驶的距离 : \n");
  float distance;
  scanf("%f",&distance);
  printf("请输入所花费的时间 : \n");
  float time;
  scanf("%f",&time);
  float speed=distance/time;
  printf("平均速度 = %f",speed);
  return 0;
}
```

## 2.6

```c
#include<stdio.h>
#include<time.h>
int main(){
  time_t t;
  // 不是基本数据类型
  time(&t);
  printf("\n 当前系统日期时间: %s", ctime(&t));
  return 0;
}
```

## 2.7

```c
#include <stdio.h>
int add(int a,int b){return a+b;}
int sub(int a,int b){
  if(a>=b)return a-b;
  else return b-a;
}
int main(){
  printf("20 + 10 = %d\n",add(20,10));
  printf("20 - 10 = %d\n",sub(20,10));
  return 0;
}
```

## 2.8

```c
#include <stdio.h>
int main(int argc, const char * argv[]) {
  printf("Name : Qbyte\n");
  printf("|-------------------------------|\n");
  printf("|Adress : KP-7,KIIT,Odisha,India|\n");
  printf("|-------------------------------|\n");
  return 0;
}
```

## 2.9

```c
#include <stdio.h>
int main(int argc, const char * argv[]) {
  printf("*\n");
  printf("*\t*\n");
  printf("*\t*\t*\n");
  printf("*\t*\t*\t*");
  return 0;
}
```

## 2.10

```c
#include <stdio.h>
int main() {
  printf(" ----------                 ----------------------\n");
  printf("|                                    |\n");
  printf("|                        ------------>>----------->             |\n");
  printf("|                                                                        |\n");
  printf("0\n");
  return 0;
}
```

## 2.11

```c
#include <stdio.h>
int main() {
  printf("3 of


, a,,;
  

f("%f",&a,c);
  float s=(a+b+c)/2;
  float area=sqrt(s-a)*(s-b)*(s-c));
  printf("Area =3f",area);
  return 0;
}
```

## 2.12

```c
#include <stdio.h>
int main() {
  printf("Enter 2 numbers");
  float x,y;
  scanf("%f %f",&x,&y);
  printf("x+y = %f\n",x+y);
  printf("x-y = %f\n",x-y);
  printf("x*y = %f\n",x*y);
  printf("x/y = %f\n",x/y);
  return 0;
}
```

## 2.13

```c
#include <stdio.h>
int main() {
  printf("Enter first coordinates");
  float x1,y1,x2,y2;
  scanf("%f %f",&x1,&y1);
  printf("Enter second coordinates");
  scanf("%f %f",&x2,&y2);
  float D=sqrt(pow((x2-x1),2)+pow((y2-y1),2));
  printf("Distance = %f",D);
  return 0;
}
```

## 2.14

```c
#include <stdio.h>
int main() {
  float radius=sqrt(25+16);
  //distance = (4-0)²+(5-0)²
  float perimeter=2*3.14159265*radius;
  float area=3.14159265*radius*radius;
  printf("Perimeter = %f\nArea = %f",perimeter,area);
  return 0;
}
```

## 2.15

```c
#include <stdio.h>
int main() {
  float radius=(sqrt(9+16))/2;
  //diameter = (5-2)²+(6-2)²
  radius=diameter/2;
  float area=3.14159265*radius*radius;
  printf("Area = %f",area);
  return 0;
}
```

# Interview Questions

- Structured approach
- Portable
- Use of pointers : directly manage memory
- Recursion : Call a function within a function
- Semicolon(`;`)
- No.
- Braces `{}`
- `main()`

