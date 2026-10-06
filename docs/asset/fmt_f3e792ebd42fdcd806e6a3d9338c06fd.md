
```c
/* 获取应用程序显示配置 */
getConfiguration()
{
FILE *fast;
fast=fopen("lastcfg.dat","r+");
if(fast==NULL)
{
    SetDefaultColor();
    return 0;
}
rewind(fast);
```

```c
/* 读取第一条记录 */
read(&clr,clsize,1,fast);
#ifdef OK
if(strcmp(clr.cfg_name,"lastcfg")!=0)
{
    SetDefaultColor();
    fclose(fast);
    return 0;
}
#endif
clr.mboxdrclr=clr.mboxdrclr;
clr.mboxbgclr=clr.mboxbgclr;
clr.fgframeclr=clr.fgframeclr;
clr.menutxbgclr=clr.menutxbgclr;
clr.menutfgclr=clr.menutfgclr;
clr.appframeclr=clr.appframeclr;
clr.section1_symb=clr.section1_symb;
clr.section1_bgclr=clr.section1_bgclr;
clr.section1_fgclr=clr.section1_fgclr;
clr.section2_symb=clr.section2_symb;
clr.section2_bgclr=clr.section2_bgclr;
clr.section2_fgclr=clr.section2_fgclr;
close(fast);
return 1;
}
```

```c
/* 设置应用程序默认颜色设置 */
SetDefaultColor()
{
    mboxdrclr=BLUE,mboxbgclr=GREEN,WHITE;
    menutxbgclr=BLUE,menutfgclr=BLUE,appframeclr=CYAN;
    section1_symb=BLUE,section1_bgclr=BLUE,section1_fgclr=BLUE;
    section2_symb=BLUE,section2_bgclr=BLUE,section2_fgclr=BLUE;
    return 1;
}
```

```c
/* 为文本添加动画 */
BlinkText(const int r,const int c,char txt[],int bgclr,int fgclr,int BGCLR2,int FGCLR2,int blink,const int dly)
```

```c
int len=strlen(txt);

BGCLR2=bgclr,FGCLR2=BLUE;
htskin(r,c,len,bgclr,fgclr,0);
print2screen(r,c,txt,bgclr,fgclr,blink);

write2screen(r,counter+1,txt[anticounter+0],BGCLR2,FGCLR2,0);
write2screen(r,counter+2,txt[anticounter+1],BGCLR2,FGCLR2,0);
write2screen(r,counter+3,txt[anticounter+2],BGCLR2,FGCLR2,0);
write2screen(r,counter+4,txt[anticounter+3],BGCLR2,FGCLR2,0);
write2screen(r,counter+5,txt[anticounter+4],BGCLR2,FGCLR2,0);
write2screen(r,counter+6,txt[anticounter+5],BGCLR2,FGCLR2,0);

delay(dly);

anticounter++;
if(anticounter >= len) anticounter=0;

return;
}
```

# 麦格罗-希尔公司

附录 IV 507

```c
write2screen(row++,column,symb,bg_color,fg_color,blink); /*打印一个符号*/
return;
)
```

* 显示一个消息框/

```c
messagebox(int row,int column,char message[50],char heading[10],char symb,int bordercl,int bg_color,int fg_color,int blink)

int len;
char key[1000];
len=strlen(message);
capture_image(row,column,row+3,column+len+7,&image);
drawbox(row,column,row+3,column+len+7,symb,bordercl,YELLOW,bordercl,YELLOW,bordercl);
fillcolor(row+1,column,row+2,column+6,"",bg_color,fg_color,0);
print2screen(row+1,column+2,bg_color,fg_color,blink);
print2screen(row+2,column+2,"Press Any Key...","bg_color,fg_color,blink);
print2screen(row,column+1,heading,bordercl,fg_color,blink);
sound(400);
delay(200);
nosound();
fflush(stdin);
key=getch();
put_image(row,column,row+3,column+len+7,&image);
return key;
```

* 填充颜色区域/

```c
fillcolor(int top_row,int left_column,int bottom_row,int right_column,char symb,int bg_color,int fg_color,int blink)
{
int i;
for(i=top_row;i<=bottom_row;i++)
    htskin(i,left_column,symb,right_column-left_column+1,bg_color,fg_color);
```

* 打印带有适当消息的消息框/

```c
drawbox(int row,int column,int brow,int bcolumn,char hsymb,char vsymb,int hbg_color,int hfg_color,int hblink,int vbg_color,int vfg_color,int vblink)
{
htskin(trow,tocol,hsymb,bcolumn-trow,hbg_color,hfg_color,hblink);
htskin(brow,column,hsymb,bcolumn-brow,hbg_color,hfg_color,hblink);
```

# 麦格罗-希尔公司

508 ANSI C 编程

```c
vtskin(trow,tcolumn,vsymb,blow-row+1,vbg_color,vfg_color,vblink);
vtskin(trow,bcolumn,vsymb,blow-row+1,vbg_color,vfg_color,vblink);
return;
```

```c
/* 在文本框下方复制 txt 图像 */
capture_image(int toprow, int leftcolumn, int bottomrow, int rightcolumn, int image)
{
  char *vidmem;
  int i,j,count;
  count=0;
  for(i=toprow;i<=bottomrow; i++)
    for(j=leftcolumn;j<=rightcolumn; j++)
    {
      vidmem=(char*)0x8800000+(i*160)+(j*2); /* 计算行与列对应的视频内存 */
      image[count]=vidmem;
      image[count+1]=(vidmem+1);
      count++;
    }
  return;
}
```

```c
/* 将图像置于屏幕上 */
put_image(int toprow, int leftcolumn, int bottomrow, int rightcolumn, int image[])
{
  char *ptr=(char*)0x88000000;
  char *vid;
  int i,j,count;
  count=0;
  for(i=toprow;i<=bottomrow; i++)
    for(j=leftcolumn;j<=rightcolumn; j++)
    {
      ptr+(i*160)+(j*2); /* 计算行与列对应的视频内存地址 */
      *vid=image[count];
      *(vid+1)=image[count+1];
      count++;
    }
  return;
}
```

/* 将光标位置移动到所需位置*/

```c
gotopapos(int r,int c)
{
    union REGS i,o;
    i.h.ah=2;
    i.h.bh=0;
    i.h.dhr;
    i.h.dl=c;
    int86(16,&i);
    return 0;
}
```

union REGS i,o;

/* 初始化鼠标*/

```c
initmouse()
{
    i.x.ax=0;
    int86(0x33,&i);
    return(o.x);
}
```

/* 显示鼠标指针*/

```c
showmouseptr()
{
    i.x.ax=1;
    int86(0x33,&i);
    return;
}
```

/* 获取鼠标位置*/

```c
getmousepos(int button,int x,int y)
{
    i.x.ax=3;
    int86(0x33,&i);
    *button=o.x;
    *x=o.y;
    *y=o.h;
    return 0;
}
```

```c
/* 恢复默认模式*/
setdefaultmode()
{
  set25x80();
  return;
}
```

```c
/* 设置屏幕的默认颜色*/
setdefaultcolor()
{
  int i;
  char far *vidmem=(char far*)0x880000;
  clr(1,80,25);
  for(i=1;i<4000;i+=2) {
    *(vidmem+i)=7;
  }
  return;
}
```

```c
/* 设置 25x80 模式*/
set25x80()
{
  asm ax,0003;
  asm int 10;
  return;
}
```

麦格罗-希尔公司

附录 IV 511

附录 IV 513

514 ANSI C 编程

附录 IV 515

# 库存管理系统

+ 1: 添加物品 物品代码: 200

2: 编辑物品信息

3: 显示物品信息

4: 查看库存报告

5: 从库存中提取物品

6: 查看待订单物品

8: 关闭应用程序

物品代码: 200

物品名称: 台式电脑

单价: 450.00

库存数量: 6.0000

订货水位: 2009

按任意键...

总物品数: 1

# 库存管理系统

+ 1: 添加物品 物品代码: 200

2: 编辑物品信息

3: 显示物品信息

4: 查看库存报告

5: 从库存中提取物品

6: 查看待订单物品

8: 关闭应用程序

物品代码: 200

物品名称: 台式电脑

单价: 450.00

库存数量: 6.0000

订货水位: 2009

按任意键...

输入数量: 2

总物品数: 1

# 麦格罗-希尔公司

518 ANSI C 编程

# 麦格罗-希尔公司

附录 IV 519

# 记录输入系统

# 库存管理系统

+ 1: 添加物品

2: 编辑物品信息

3: 显示物品信息

4: 查看库存报告

5: 从库存中提取物品

6: 查看待订单物品

8: 关闭应用程序

记录输入系统的目标是开发一个基于登录的记录系统，该系统为不同的用户组提供了标题化界面。应用程序为管理员和员工提供了菜单。根据用户的选择，将提示用户输入其姓名和密码。例如，员工在用密码登录后可以记录他的进入和离开时间。该项目还对用户输入进行了验证，以确保数据输入数据库。该项目使用了多种 C 概念，如 `while` 循环、`if` 语句和 `switch` 分来显示所需的功能。

# 记录输入系统

在 Borland C++ 3.0 上编译

```c
#include <stdio.h>
#include <conio.h>
#include <string.h>
#include <dos.h>
#include <ctype.h>

void dataentry(void);
void selectOption(void);
void getData(int option);

void main()
{
    int cancelOption,timeOption,exitOption;
    char choice[];
    char selectOption[1];

    textcolor(YELLOW);
    cancelOption=0;
    while (cancelOption==0)
    {
        clrscr();
        gotoxy(30,7);
        printf("请选择操作->");
        gotoxy(30,10);
        printf("每日记录 [1] *");
        gotoxy(30,11);
        printf("数据输入 [2] *");
        gotoxy(30,12);
        printf("关闭 [3] *");
        gotoxy(30,15);
        printf("请输入您的选择 (1/2/3): *");
        scanf("%s",&choice);
    }
}
```

# 麦格希尔公司

附录 IV 523

```c
printf("您输入了无效的 PwdOption。请选择 1, 2 或 3。");
getch();
cancelOption=0;
}

clrcr();
gotoxy(2,13);
printf("应用程序将现在关闭。谢谢！");
getch();

/* 此函数为系统执行的数据输入提供逻辑。
仅允许管理员用户访问数据输入项。*/
void dataentry(void)
{
char adminName[10], passwd[5],buffer[1];
char temp[6],sel[1];
int validNameOption,validPwdOption,returnOption,UserName,tmp;
char plus;
clrcr();
validUserNameOption=0;
validUserPwdOption=0;
while (validUserPwdOption==0)
{
    clrcr();
    while (validUserNameOption==0)
    {
        clrcr();
        gotoxy(20,5);
        printf("IT 数据录入系统-管理员界面");
        printf("信息：输入 return 返回主屏幕。");
        gotoxy(28,10);
        printf("输入管理员名称： ");
        scanf("%s",&adminName);
        returnOption=strcmp(adminName,"return");
        UserName=strcmp(adminName,"admin");
        if (returnOption==0)
        {}
}
```

# 麦格希尔公司

524 ANSI C语言编程

```c
goto stream;
}
if (!(UserName==0 || returnOption==0))
{
    gotoxy(32,11);
    printf("管理员名称无效。");
    getch();
    validUserNameOption=0;
}else
    validUserNameOption=1;
}
gotoxy(30,11);
printf("输入密码： ");
inc=0;
while (inc<5)
{
    passwd[inc]=getch();
    inc+=1;
    printf("* ");
}
inc=0;
while (inc<5)
{
    tempo[inc]=passwd[inc];
    inc+=1;
}
while(getch()!=13)
if (strcmp(tempo,"admin2")==0)
{
    gotoxy(28,13);
    printf("输入的密码错误。请重试。");
    getch();
    validUserPwdOption=0;
}else
{
    clrscr();
    gotoxy(24,11);
```

# 麦格希尔公司

附录 IV 525
