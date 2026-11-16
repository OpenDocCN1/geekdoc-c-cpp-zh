The above program will produce five beeps then display Hello world, theoretically. But the amazing fact is you will see Hello world written out there even before the first beep you will listen. Why? You may think that it takes about 0.887 milli second for sound to reach from the computer to our ears, then eardrum vibrates and then accordingly the signal is sent to our brain. While it takes, about 1.0167 nano second to reach from computer to our eye sensors and then signal is directly to our brain. So, the time lag which arises in vibrating the sensors speakers, reaching sound to our ears and then vibrating the ear drums does not arises while displaying the output. So, we see Hello World before even hearing first beep. Well, you are right but there is another strong reason behind this, If we want to perform any task using command line, it is much faster than the GUI approach. This means our GUI computers are the extended version of command line computers, and not vice versa. If anyone is thinking that his computer is much advanced having very powerful and colourful GUI, and command line is added to it externally only for those who are accustomed to it, then he has to rethink again. Well scientist is busy in extending command line to GUI but they are not working to design any computer which can perform tasks more faster in GUI than through command line. So, program pass the signal to produce the beep to operating system, then it gave the signal to display the Hello World, but the OS needs more time to convert an electrical signal to sound signal than to display. Well the speed order is as follows:

+   Command line signal>Display signal>Sound signal

# \b Backspace

Suppose you want to abolish a character on output screen. So you cannot press a backspace button there. So, we need to know the character which is equivalent to backspace character. The answer is \b .Here, you will see the reality of backspace, in programs we cannot delete like we delete files. Why? The fact is delete did not have any mathematical meaning except than abstaining from displaying the corresponding files. That’s why, whatever files you delete even from the recycle bin, are not permanently deleted and can be recovered from various simple software such as Recuva . So, the question arise how to delete a character from output screen? The answer lies in overwriting it. The \b does not overwrite the character rather it moves the cursor one space back so that you can overwrite it. Consider the following program:

```
#include<iostream>
using namespace std;
int main()
{
    cout<<"Hello\bc World";
}
```

Output