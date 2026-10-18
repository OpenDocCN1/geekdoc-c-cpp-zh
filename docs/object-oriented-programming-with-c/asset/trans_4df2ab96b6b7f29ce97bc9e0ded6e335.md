

- 分析
- 设计
- 编码
- 测试
- 维护

在面向对象范式中，系统可以被视为一组相互作用的实体集合，以实现特定目标。

在面向对象分析中，这些实体被称为对象。面向对象分析（OOA）是指用现实世界的对象、其行为以及它们之间的交互来描述软件需求的方法。

面向对象设计（OOD）将软件需求转化为对象的规范，并从中推导出可创建对象的类层次结构。

面向对象编程（OOP）是指使用面向对象编程语言（如 C++）借助对象来实现程序。

面向对象分析（OOA）方法包括以下步骤：

- 定义问题。
- 估计用户和软件的需求。
- 识别对象及其属性。
- 识别每个对象应提供的接口服务。
- 在所需服务和提供的服务方面建立对象之间的相互连接。

面向对象设计（OOD）方法涉及以下步骤：

- 审查分析阶段创建的对象。
- 指定类依赖关系。
- 组织类层次结构。
- 设计类。
- 设计成员函数。
- 设计驱动程序。

- 你可以生成尽可能正确和完整的易于理解的规范。
- 用户可以理解所提供的产品。
- 系统安装后所需的维护变更被最小化。
- 开发工程师可以从经过测试和批准的规范集中开展工作。

- 在完整系统完成之前，通过构建和测试拟议系统的可工作模型来理解系统设计及其影响的一种方法是原型。 该模型系统称为原型，该过程称为原型设计。

- 使用原型方法的优点是：

## 关键术语

| 关键术语 | 关键术语 | 关键术语 | 关键术语 | 关键术语 |
| --- | --- | --- | --- | --- |
| abstract class | abstract nouns | a-kind-of | analysis | a-part-of |
| being verbs | bubble chart | class hierarchies | classes | classic life cycle |
| classification relationship | client-server relationship | coding | collaborations | common nouns |
| compare verbs | composition relationship | containment relationship | context diagrams | data dictionary |
| data flow diagrams | decision table | decision tree | design | development tools |
| doing verbs | driver program | entities | entity relationship diagram | entity-relationship |
| first generation | flowcharts | forest model | fountain model | functional decomposition |
| grid charts | has-a relationship | having verbs | hierarchical chart | information flow diagram |
| inheritance relationship | instances of objects | is-a relationship | layout forms | loop |
| maintenance | mass nouns | member functions | message communications | methods |
| modular approach | object-oriented analysis | object-oriented design | object-oriented paradigm | object-oriented programming |
| objects | playscripts | problem definition | problem space | procedure-oriented paradigm |
| procedures | process layering | program flowcharts | proper nouns | prototype |
| prototyping | prototyping paradigm | second generation | selection | sequence |
| single-tree model | software life cycle | solution space | stative verbs | structure chart |
| structured design | structured tools | system flowcharts | testing | textual analysis |
| third generation | tools | top-down approach | traditional tools | use relationship |
| Warnier diagrams | water-fall model |  |  |  |

## 复习问题

- 17.1 列出你认为软件开发人员在设计系统时应牢记的五项最重要的特性。
- 17.2 描述为什么软件测试很重要。
- 17.3 列出过程导向和面向对象范式之间的主要区别。
- 17.4 你如何理解软件维护？ 何时以及如何进行？
- 17.5 系统开发生命周期的每个阶段的主要参与者是谁？
- 17.6 在分析阶段是否有必要研究现有系统？ 如果有，为什么？ 如果没有，为什么不？
- 17.7 经典软件开发生命周期的局限性是什么？
- 17.8 “软件开发过程是一个迭代过程”。 讨论。
- 17.9 区分“瀑布”模型和“喷泉”模型。

- **(g)** 结构化编程技术在面向对象程序设计中没有立足之地。
- **(h)** 原型不能改进为最终产品。

## 项目

### 打字导师应用程序

```cpp
/*Header Files*/
#include<iostream.h>
#include<fstream.h>
#include<iomanip.h>
#include<stdio.h>
#include<conio.h>
#include<process.h>
#include<ctype.h>
#include<time.h>
/*Function Prototypes*/
void tips(void);
void practice(void);
void test(void);

void main()
{
    char choice;

    while(1)
    {
    clrscr();
    gotoxy(33,5);
    cout<<"Typing Tutor";
    gotoxy(33,6);
    cout<<"_______________________";
    gotoxy(30,8);
    cout<<"1 - Typing Tips";
    gotoxy(30,10);
    cout<<"2 - Typing Practice";
    gotoxy(30,12);
    cout<<"3 - Typing Test";
    gotoxy(30,14);
    cout<<"4 - Exit";
    gotoxy(30,30);
    cout<<"Enter your choice";

    choice=getch();
    switch(choice)
    {
    case('1'):
    tips();
    break;
    case('2'):
    practice();
    break;
    case('3'):
    test();
    break;
    case('4'):
    clrscr();
    exit(1);
    break;
    default:
    gotoxy(30,30);
    clreol();
    cout<<"Invalid Choice..";
    gotoxy(30,31);
    cout<<"Press any key to continue..";
    getch();
    } //End of switch-case block
    } //End of while block
} //End of main()
/*Function for displaying typing tips*/
void tips(void)
{
    clrscr();
    gotoxy(2,3);
    cout<<"Typing tips";
    gotoxy(2,4);
    cout<<"________________";

    gotoxy(2,6);
    cout<<"1. First and foremost, make sure that you are seated comfortably with the ";
    gotoxy(5,7);
    cout<<"keyboard placed at appropriate height.";

    gotoxy(2,9);
    cout<<"2. Use all your fingers while typing, with the thumb being used for pressing ";
    gotoxy(5,10);
    cout<<"the space bar";
    gotoxy(2,12);
    cout<<"3. Explore the various keys present on the keyboard and gradually try to build ";
    gotoxy(5,13);
    cout<<"your finger memory.";

    gotoxy(2,15);
    cout<<"4. Avoid looking at the keyboard while typing and try to keep your eyes on the ";
    gotoxy(5,16);
    cout<<"screen.";

    gotoxy(2,18);
    cout<<"5. Practice as much as you can to build your typing skills.";

    gotoxy(30,30);
    cout<<"Press any key to go back..";
    getch();
}

/*Function for practicing typing*/
void practice(void)
{
    char ch1,ch2;
    int count,noc;
    fstream fptr1,fptr2;

    while(1)
    {
        count=0;
        noc=0;
        clrscr();
        fptr1.open("practice.txt",ios::in);

        gotoxy(2,2);
        while(fptr1)
        {
            fptr1.get(ch1);
            cout<<ch1;
            noc++;
        }
        fptr1.close();

        fptr2.open("type1.txt",ios::out);

        gotoxy(2,6);
        cout<<"Type the above text";

        gotoxy(2,8);

        time_t t1;
        time(&t1);

        for(int i=0;i<44;i++)
        {
            ch2=getche();
            fptr2.put(ch2);
        }
        time_t t2;
        time(&t2);

        fptr2.close();

        fptr1.open("practice.txt", ios::in);
        fptr2.open("type1.txt", ios::in);

        gotoxy(25,25);
        cout<<"Typing Practice Results...";

        gotoxy(25,27);
        int flag=0;
        int flag2=0;
        int flag3=0;
        for(i=0;i<44;i++)
        {
            fptr1.get(ch1);
            fptr2.get(ch2);
            if(flag==5)
            {
                while(1)
                {
                    if(flag2==0)
                        fptr1.get(ch1);
                    if(flag3==0)
                        fptr2.get(ch2);
                    if(ch1==' ')
                        flag2=1;
                    if(ch2==' ')
                        flag3=1;
                    if(flag2==1 && flag3==1)
                        break;
                } //End of while block
            }
        }
```
