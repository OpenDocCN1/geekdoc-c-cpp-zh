```
```c
write2screen(r,c+animcounter+6,txt[animcounter+5],bgclr,fgclr,0);

animcounter+=1;
if(animcounter+5 >= len) animcounter=0;


return;
}

/* Displays a single character with its attribute*/
write2screen(int row,int col,char ch,int bg_color,int fg_color,int blink)
{
 int attr;
 char far *v;
 char far *ptr=(char far*)0xB8000000;
 if(blink!=0)
    blink|=128;

 attr=bg_color+blink;

 attr=attr<<4;
 attr+=fg_color;
 attr+=attr<<8;
 v=ptr+row*160+col*2;  /*Calculates the video memory address corresponding to row & column*/
 *v=ch;
 v++;
 *v=attr;
 return 0;
}

/* Prints text with color attribute direct to the screen*/
print2screen(int row,int col,char string[],int bg_color,int fg_color,int blink)
{
 int i=row,j=col,strno=0,len;
 len=strlen(string);
 while(j<80)
 {
    j++;
    if(j==79)
    {
    j=0;
    i+=1;
```
```