![](cover.jpeg)

Gaming in Turbo C++ with Mouse Programming -

Suit 16

BY: PRASENJIT DAS

Introduction

"Suit 16" game comprises of 16 face cards out of the deck of 52 cards. The aim of the game is to collect 4 face cards of same suit in the maximum of 10 moves. There are four suits in the deck of 52 cards which are Spade, Club, Heart and Diamond. There are 13 cards in each suit out of which 9 cards show numbers from 1 to 9 and rest of four are the face cards namely “Ace”, “Joker”, “Queen” and “King”. So, collectively from the four suits, there are 16 face cards, which have been used in this game.

GAME EXECUTION

The game starts with a welcome screen showing the name of the game with 16 face cards. The welcome screen is as shown below:

![](images/00001.jpeg)

The welcome screen is followed by the main screen of the game. Here onwards, the mouse click works as the input. The main screen of the game is as shown below:

![](images/00002.jpeg)

The main screen consists of 4 main buttons which are “Play Game”, “Instructions”, “About Game” and “Exit”. The user exits the game on clicking the “Exit” button. On clicking the “About Game” button, the information about the game is displayed which is as shown below:

![](images/00003.jpeg)

On clicking the “Instructions” button, the instructions for playing the game is displayed which is as shown below:

![](images/00004.jpeg)

On clicking the “Play Game” button, the game starts with a loading screen. The game loading screen is as shown below:

![](images/00005.jpeg)

The loading screen has been designed such that a person is approaching towards the game. After the loading animation, two buttons namely “Proceed” and “Abort” is displayed, where user has the option whether to proceed with the game or abort from the program. The “Abort” button is displayed all the time till the completion of the game so that the user has the option to abort from the program at any point of time.

![](images/00006.jpeg)

On clicking the “Proceed” button, the next screen displayed is the card selection screen in which the user has to select 4 cards out of the total of 16 cards. The card selection screen is as shown below:

![](images/00007.jpeg)

The actual game starts after the user has selected the four cards. The game screen is as shown below:

![](images/00008.jpeg)

After user has selected his 4 cards, the rest of the 8 cards become reserve cards. There are 10 moves available in total in which the user has to collect 4 cards of same suit by replacing one card with one of the 8 reserve cards. Before each move, the reserve cards are reshuffled. The user looses the game if he is unable to collect 4 cards of same suit within 10 moves. After the game is finished, the main screen with 4 main buttons reappears.

PROGRAM LISTING

#include<conio.h>

#include<graphics.h>

#include<stdio.h>

#include<string.h>

#include<stdlib.h>

#include<dos.h>

#include<process.h>

struct p

{ char suit[2];

  char card[2];

  int color;

  int rev_color;

};

p pack[16]={ {3,'\0',"K",4,10},{3,'\0',"Q",4,10},

     {3,'\0',"J",4,10},{3,'\0',"A",4,10},

     {4,'\0',"K",4,10},{4,'\0',"Q",4,10},

     {4,'\0',"J",4,10},{4,'\0',"A",4,10},

     {5,'\0',"K",0,15},{5,'\0',"Q",0,15},

     {5,'\0',"J",0,15},{5,'\0',"A",0,15},

     {6,'\0',"K",0,15},{6,'\0',"Q",0,15},

     {6,'\0',"J",0,15},{6,'\0',"A",0,15}

   };

int bin[16];

int rdm[16] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15};

int pl[4],res[12];

void design(int i, int j, int k)

{

  setfillstyle(1,15);

  setcolor(6);

  rectangle(i,j,i+70,j+90);

  floodfill(i+1,j+1,6);

  setcolor(pack[k].color);

  settextstyle(0,0,2);

  outtextxy(i+60,j+10,pack[k].suit);

  outtextxy(i+10,j+80,pack[k].suit);

  settextstyle(7,0,6);

  outtextxy(i+35,j+40,pack[k].card);

}

void design_rev(int i, int j, int k)

{

  setfillstyle(1,0);

  setcolor(6);

  rectangle(i,j,i+70,j+90);

  floodfill(i+1,j+1,6);

  setcolor(pack[k].rev_color);

  settextstyle(0,0,2);

  outtextxy(i+60,j+10,pack[k].suit);

  outtextxy(i+10,j+80,pack[k].suit);

  settextstyle(7,0,6);

  outtextxy(i+35,j+40,pack[k].card);

}

void design_bk(int i, int j)

{

  setcolor(6);

  rectangle(i,j,i+70,j+90);

  line(i+35,j,i+70,j+45);

  line(i+70,j+45,i+35,j+90);

  line(i+35,j+90,i,j+45);

  line(i,j+45,i+35,j);

  rectangle(i+17,j+22,i+53,j+68);

  circle(i+35,j+45,11);

  setfillstyle(9,9);

  floodfill(i+1,j+1,6);

  floodfill(i+69,j+1,6);

  floodfill(i+69,j+89,6);

  floodfill(i+1,j+89,6);

  setfillstyle(2,9);

  floodfill(i+35,j+2,6);

  floodfill(i+68,j+45,6);

  floodfill(i+35,j+88,6);

  floodfill(i+2,j+45,6);

  setfillstyle(6,9);

  floodfill(i+40,j+28,6);

  setfillstyle(9,9);

  floodfill(i+35,j+45,6);

}

void welcome()

{

  int i,j;

  int m[7]={130,146,164,174,196,220,246};

  rectangle(1,1,639,479);

  rectangle(6,6,634,474);

  setfillstyle(1,2);

  floodfill(7,7,15);

  settextstyle(1,0,5);

  settextjustify(1,1);

  setcolor(14);

  outtextxy(320,235,"SUIT 16");

  for(i=70,j=0;i<=490;i+=140,j++)

    {

      design(i,10,j);

      design(i,380,j+12);

    }

  for(i=40,j=0;i<=170;i+=130,j++)

    {

      design(i,120,j+4);

      design(i,270,j+6);

      design(i+340,120,j+8);

      design(i+340,270,j+10);

    }

  setcolor(14);

  for(i=40,j=580;i<=580;i++,j--)

    {

      sound(2*i);

      setcolor(14);

      line(40,215,i,215);

      line(j,265,580,265);

      delay(5);

    }

  while(!kbhit())

    {

      j=random(7);

      sound(m[j]*4);

      delay(100);

    }

  nosound();

  getch();

  setcolor(2);

  for(i=0;i<=313;i++)

    {

      rectangle(7+i,7,633-i,473);

      delay(5);

    }

}

void button(int i, int j, char *st)

{

  setcolor(15);

  rectangle(i+1,j,i+154,j+26);

  setfillstyle(1,7);

  floodfill(i+2,j+1,15);

  setcolor(0);

  rectangle(i+2,j+26,i+155,j+27);

  rectangle(i+154,j,i+155,j+26);

  settextstyle(4,0,1);

  outtextxy(i+79,j+9,st);

}

void reverse(int i, int j)

{

  setcolor(0);

  rectangle(i+1,j,i+154,j+26);

  setcolor(15);

  rectangle(i+2,j+26,i+155,j+27);

  rectangle(i+154,j,i+155,j+26);

}

void forward(int i, int j)

{

  setcolor(15);

  rectangle(i+1,j,i+154,j+26);

  setcolor(0);

  rectangle(i+2,j+26,i+155,j+27);

  rectangle(i+154,j,i+155,j+26);

}

union REGS in,out;

void initmouse()

{

  in.x.ax=0;

  int86(51,&in,&out);

}

void callmouse()

{

  in.x.ax=1;

  int86(51,&in,&out);

}

void mousehide()

{

  in.x.ax=2;

  int86(51,&in,&out);

}

void limit(int x1, int y1, int x2, int y2)

{

  in.x.ax=7;

  in.x.cx=x1;

  in.x.dx=x2;

  int86(51,&in,&out);

  in.x.ax=8;

  in.x.cx=y1;

  in.x.dx=y2;

  int86(51,&in,&out);

}

void mousepos(int *c, int *x, int *y)

{

  in.x.ax=3;

  int86(51,&in,&out);

  *c=out.x.bx;

  *x=out.x.cx;

  *y=out.x.dx;

}

void rt_clk()

{

  setfillstyle(1,10);

  floodfill(158,425,15);

  settextstyle(7,0,1);

  setcolor(4);

  outtextxy(388, 445, "Right Click Not Allowed.");

}

void hd_bd(int x)

{

  int i=8;

  setcolor(i);

  ellipse(x+7,204,280,0,10,15);

  ellipse(x,224,320,50,3,7);

  ellipse(x+12,224,130,270,3,7);

  ellipse(x+17,211,250,90,3,2);

  line(x,228,x+15,232);

  int poly[] = {x+12, 204, x+10, 207, x+8, 208, x+8, 210, x+7, 207, x+5, 207, x+3, 210, x+3, 218, x-5, 212, x-4, 204};

  drawpoly(10,poly);

  ellipse(x+7,200,0,180,10,5);

  ellipse(x+7,204,0,180,20,5);

  line(x-13,204,x+27,204);

  setfillstyle(1,8);

  floodfill(x+1,207,i);

  setfillstyle(1,14);

  floodfill(x+13,209,i);

  floodfill(x+18,211,i);

  setfillstyle(1,4);

  floodfill(x+7,203,i);

  setfillstyle(1,2);

  floodfill(x+7,197,i);

  setfillstyle(1,0);

  fillellipse(x+14,210,1,2);

  arc(x+14,210,70,160,3);

  ellipse(x+14,217,70,180,4,3);

  setfillstyle(1,8);

  floodfill(x+12,215,i);

  line(x,227,x+15,232);

  line(x+15,232,x+17,237);

  line(x+17,237,x,232);

  line(x,232,x,227);

  setfillstyle(1,4);

  floodfill(x+3,230,i);

  ellipse(x+7,292,20,70,15,60);

  ellipse(x+8,283,120,170,15,60);

  line(x-7,273,x+21,272);

  setfillstyle(1,2);

  floodfill(x-3,269,i);

}

void stand(int x)

{

  hd_bd(x);

  int i=8;

  setcolor(i);

  int hnd[] = {x+9, 249, x+11, 239, x+1, 239, x+1, 250, x+7, 264, x+15, 264, x+7, 249};

  drawpoly(7,hnd);

  int plm[] = {x+9, 265, x+10, 267, x+16, 267, x+14, 265};

  drawpoly(4,plm);

  setfillstyle(1,14);

  floodfill(x+12,266,i);

  setfillstyle(1,3);

  floodfill(x+7,244,i);

  line(x+15,274,x+13,294);

  line(x-1,274,x+1,294);

  line(x+15,274,x-1,274);

  line(x+13,294,x+1,294);

  setfillstyle(1,12);

  floodfill(x+7,279,i);

  setfillstyle(1,8);

  ellipse(x+10,299,0,180,10,3);

  line(x,299,x+20,299);

  floodfill(x+10,298,8);

}

void one(int x)

{

  int i=8;

  setcolor(i-1);

  int bkhnd[] = {x-17, 252, x-8, 246, x-15, 239, x-23, 247, x-28, 261, x-23, 267, x-18, 250};

  drawpoly(7,bkhnd);

  int bkplm[] = {x-28, 263, x-28, 265, x-24, 269, x-24, 267};

  drawpoly(4,bkplm);

  setfillstyle(1,14);

  floodfill(x-27,264,i-1);

  setfillstyle(1,3);

  floodfill(x-15,244,i-1);

  setcolor(i);

  setfillstyle(1,12);

  int lgft[] = {x+1, 273, x+11, 295, x-1, 295, x-13, 273, x+1, 273};

  drawpoly(5,lgft);

  floodfill(x-6,276,i);

  setfillstyle(1,8);

  ellipse(x+10,299,0,180,10,3);

  line(x,299,x+20,299);

  floodfill(x+10,298,i);

}

void two(int x)

{

  int i=8;

  setcolor(i-1);

  int fthnd[] = {x-2, 240, x-8, 232, x-15, 239, x-7, 247, x+7, 252, x+13, 247, x-4, 241};

  drawpoly(7,fthnd);

  int ftplm[] = {x+9, 252, x+11, 252, x+15, 248, x+13, 248};

  drawpoly(4,ftplm);

  setfillstyle(1,14);

  floodfill(x+11,251,i-1);

  setfillstyle(1,3);

  floodfill(x-13,239,i-1);

  setcolor(i-1);

  setfillstyle(1,12);

  int lgbk[] = {x-4, 273, x-20, 273, x-22, 295, x-12, 295, x-4, 273};

  drawpoly(5,lgbk);

  floodfill(x-16,276,i-1);

  setcolor(i);

  setfillstyle(1,8);

  ellipse(x-12,299,0,180,10,3);

  line(x-2,299,x-22,299);

  floodfill(x-12,298,i);

}

void ltlg(int x)

{

  one(x);

  hd_bd(x-16);

  two(x);

}

void rtlg(int x)

{

  two(x);

  hd_bd(x-16);

  one(x);

}

void loading_scr()

{

  int i,st=1,lr=0;

  setcolor(6);

  rectangle(20,70,610,375);

  setcolor(15);

  rectangle(21,71,609,374);

  setfillstyle(1,0);

  floodfill(25,75,15);

  rectangle(30,300,600,320);

  line(21,330,609,330);

  settextstyle(4,0,2);

  setcolor(14);

  settextjustify(1,1);

  outtextxy(315,350,"Approaching to game..");

  setfillstyle(6,14);

  floodfill(35,310,15);

  for(i=40;i<=578;i+=22)

    {

       if(st)

{

   if(i>40)

     i-=22;

   stand(i);

   st=0;

}

       else

{

   if(lr)

     {

       rtlg(i);

       lr=0;

     }

   else

     {

       ltlg(i);

       lr=1;

     }

   st=1;

}

       delay(200);

       setfillstyle(1,0);

       floodfill(25,75,15);

    }

  setfillstyle(1,0);

  floodfill(315,335,15);

}

void exit_game()

{

  int i;

  mousehide();

  for(i=0;i<=240;i++)

    {

      rectangle(i,i,640-i,480-i);

      delay(5);

    }

  closegraph();

  exit(0);

}

void loading()

{

  int x,y,c,op=0;

  mousehide();

  loading_scr();

  button(270,385,"Proceed");

  button(450,385,"Abort");

  limit(200,380,600,410);

  callmouse();

  while(!op)

    {

      mousepos(&c,&x,&y);

      if(c&2)

{

  rt_clk();

  do

    {

      mousepos(&c,&x,&y);

    } while(c&2);

  setfillstyle(1,2);

  floodfill(158,426,15);

}

      if(c&1)

{

  if((y>386)&&(y<410))

    {

      if((x>271)&&(x<424))

{

  op=1;

  reverse(270,385);

}

      else if((x>451)&&(x<604))

{

  op=2;

  reverse(450,385);

}

    }

  else

    {

      switch(op)

{

  case 1: forward(270,385);

  break;

  case 2: forward(450,385);

}

      op=0;

    }

  do

    {

      mousepos(&c,&x,&y);

    } while(c&1);

}

    }

  switch(op)

    {

      case 1: forward(270,385);

      mousehide();

      setfillstyle(1,0);

      floodfill(25,75,6);

      setcolor(8);

      rectangle(250,382,610,414);

      setfillstyle(1,3);

      floodfill(251,383,8);

      setfillstyle(1,10);

      floodfill(25,75,15);

      setfillstyle(1,2);

      floodfill(25,75,15);

      break;

      case 2: forward(450,385);

      exit_game();

      exit(0);

    }

}

void rndm()

{ int i,j,k,a,c;

  for(i=0;i<16;i++)

     { c=16-i;

       randomize();

       a=rdm[(int)(rand()%c)];

       for(j=0;j<c;j++)

  { if(a==rdm[j])

{ for(k=j;k<(c-1);k++)

    rdm[k]=rdm[k+1];

  rdm[c-1]=a;

  break;

}

  }

     }

}

void shuffle()

{ int i,j,k,a,c;

  for(i=0;i<12;i++)

     { c=12-i;

       randomize();

       a=res[(int)(rand()%c)];

       for(j=0;j<c;j++)

  { if(a==res[j])

{ for(k=j;k<(c-1);k++)

    res[k]=res[k+1];

  res[c-1]=a;

  break;

}

  }

     }

}

void select()

{

  int x,y,x1,y1,c,crd=1,j=16;

  for(int i=40;i<=540;i+=100)

    { design_bk(i,70);

      delay(20);

      design_bk(i,190);

      delay(20);

      if(i<=340)

{

  design_bk(i,310);

  delay(20);

}

    }

  button(450,380,"Abort");

  limit(30,50,610,400);

  callmouse();

  setfillstyle(1,6);

  floodfill(158,425,15);

  settextstyle(7,0,1);

  setcolor(14);

  outtextxy(388,445,"Select any 4 cards.");

  rndm();

  while(crd<=4)

    {

      mousepos(&c,&x,&y);

      if(c&2)

{

  rt_clk();

  do

    {

      mousepos(&c,&x,&y);

    } while(c&2);

  setfillstyle(1,6);

  floodfill(158,425,15);

  settextstyle(7,0,1);

  setcolor(14);

  outtextxy(388,445,"Select any 4 cards.");

}

      if(c&1)

{

  if((x>451)&&(x<604)&&(y>380)&&(y<406))

    {

      crd=6;

      reverse(450,380);

    }

  for(i=40;i<=540;i+=100)

    {

      if((x>i)&&(x<(i+70)))

{

  if(((y>70)&&(y<160))||

                    ((y>190)&&(y<280))||

          ((i<=340)&&(y>310)&&(y<400)))

    {

      j=((x-40)/100)+(((y-70)/120)*6);

      x1=i;

      if((y>70)&&(y<160))

y1=70;

      else if((y>190)&&(y<280))

y1=190;

      else y1=310;

      break;

    }

}

    }

  if(bin[j]==1)

    {

      j=17;

      setfillstyle(1,10);

      floodfill(158,425,15);

      settextstyle(7,0,1);

      setcolor(4);

      outtextxy(388,445,"Card already selected.");

    }

  do

    {

      mousepos(&c,&x,&y);

    } while(c&1);

}

      setfillstyle(1,6);

      floodfill(158,425,15);

      settextstyle(7,0,1);

      setcolor(14);

      outtextxy(388,445,"Select any 4 cards.");

      if((j<16)&&(!(bin[j])))

{

  mousehide();

  bin[j]=1;

  setcolor(15);

  rectangle(x1,y1,x1+70,y1+90);

  setfillstyle(1,4);

  floodfill(x1+5,y1+5,15);

  pl[crd-1]=rdm[j];

  design(x1,y1,pl[crd-1]);

  crd++;

  limit(30,50,610,410);

  callmouse();

}

    }

  if(crd==6)

    {

      mousehide();

      forward(450,380);

      exit_game();

    }

}

int win_chk()

{

  if((pack[pl[0]].suit[0]==pack[pl[1]].suit[0])&&

     (pack[pl[1]].suit[0]==pack[pl[2]].suit[0])&&

     (pack[pl[2]].suit[0]==pack[pl[3]].suit[0]))

    return 1;

  else

    return 0;

}

void reserve()

{

  int a=0;

  for(int i=0;i<16;i++)

    {

      if(!bin[i])

{

  res[a]=rdm[i];

  a++;

  bin[i]=1;

}

    }

}

void play_scr()

{

  mousehide();

  setcolor(1);

  rectangle(7,46,633,423);

  setfillstyle(1,10);

  floodfill(25,75,1);

  setfillstyle(1,2);

  floodfill(25,75,15);

  setcolor(15);

  line(7,295,633,295);

  rectangle(450,295,633,350);

  line(550,295,550,350);

  settextstyle(7,0,1);

  setcolor(14);

  outtextxy(490,320,"Moves:");

  for(int i=40,a=0;i<=540;i+=100,a++)

    { design_bk(i,70);

      design_bk(i,190);

      if(i<=340)

design(i,310,pl[a]);

    }

  button(450,380,"Abort");

  setfillstyle(1,2);

  floodfill(388,425,15);

}

void shuffle_scr()

{

  int i,a,b,c,d,e,f;

  setcolor(1);

  rectangle(7,46,633,294);

  setfillstyle(1,10);

  floodfill(25,75,1);

  setfillstyle(1,2);

  floodfill(25,75,15);

  setcolor(6);

  rectangle(20,50,610,285);

  setcolor(15);

  rectangle(21,51,609,284);

  line(315,51,315,284);

  settextstyle(7,0,3);

  setcolor(14);

  settextjustify(1,1);

  outtextxy(168,160,"RESHUFFLING");

  outtextxy(168,190,"CARDS");

  for(i=1;i<=9;i++)

    {

      if(i%2)

{

  a=6;b=1;c=1;

  d=2;e=1;f=2;

}

      else

{

  a=2;b=1;c=2;

  d=6;e=1;f=1;

}

      setcolor(a);

      setfillstyle(b,c);

      rectangle(553,161,567,179);

      floodfill(560,170,a);

      rectangle(540,111,554,129);

      floodfill(547,120,a);

      rectangle(503,74,517,92);

      floodfill(510,83,a);

      rectangle(453,61,467,79);

      floodfill(460,70,a);

      rectangle(403,74,417,92);

      floodfill(410,83,a);

      rectangle(366,111,380,129);

      floodfill(373,120,a);

      rectangle(353,161,367,179);

      floodfill(360,170,a);

      rectangle(366,211,380,229);

      floodfill(373,220,a);

      rectangle(403,248,417,266);

      floodfill(410,257,a);

      rectangle(453,261,467,279);

      floodfill(460,270,a);

      rectangle(503,248,517,266);

      floodfill(510,257,a);

      rectangle(540,211,554,229);

      floodfill(547,220,a);

      setcolor(d);

      setfillstyle(e,f);

      rectangle(479,64,493,82);

      floodfill(486,73,d);

      rectangle(550,135,564,153);

      floodfill(557,144,d);

      rectangle(550,187,564,205);

      floodfill(557,196,d);

      rectangle(479,258,493,276);

      floodfill(486,267,d);

      rectangle(427,258,441,276);

      floodfill(434,267,d);

      rectangle(356,187,370,205);

      floodfill(363,196,d);

      rectangle(356,135,370,153);

      floodfill(363,144,d);

      rectangle(427,64,441,82);

      floodfill(434,73,d);

      rectangle(524,90,538,108);

      floodfill(531,99,d);

      rectangle(524,232,538,250);

      floodfill(531,241,d);

      rectangle(382,232,396,250);

      floodfill(389,241,d);

      rectangle(382,90,396,108);

      floodfill(389,99,d);

      delay(200);

    }

}

void res_scr()

{

  setcolor(1);

  rectangle(7,46,633,294);

  setfillstyle(1,10);

  floodfill(25,75,1);

  setfillstyle(1,2);

  floodfill(25,75,15);

  for(int i=40;i<=540;i+=100)

    { design_bk(i,70);

      design_bk(i,190);

    }

}

void loose()

{ int x1,x2,y1,y2,i,j,x,y,c,fin=0;

  setcolor(6);

  rectangle(20,70,610,375);

  setfillstyle(1,0);

  floodfill(25,75,6);

  button(450,385,"Finish");

  limit(440,380,600,400);

  callmouse();

  settextstyle(7,0,8);

  while(!fin)

    {

      j=random(15)+1;

      for(int k=0;k<(random(300)*10);k=k+2)

{

  setcolor(j);

  x1=21+k;

  if(x1>609)

    x1=609;

  y1=71+k;

  if(y1>374)

    y1=374;

  x2=609-k;

  if(x2<21)

    x2=21;

  y2=374-k;

  if(y2<71)

    y2=71;

  rectangle(x1,y1,x2,y2);

  setcolor(0);

  outtextxy(315,222,"You Loose");

  delay(5);

}

      mousepos(&c,&x,&y);

      if(c&2)

{

  rt_clk();

  do

    {

      mousepos(&c,&x,&y);

    } while(c&2);

  setfillstyle(1,2);

  floodfill(158,426,15);

}

      if(c&1)

{

  if((x>451)&&(y>385)&&(x<604)&&(y<411))

    {

      fin=1;

      reverse(450,385);

    }

  else

    {

      fin=0;

      forward(450,385);

    }

  do

    {

      mousepos(&c,&x,&y);

    } while(c&1);

}

    }

  mousehide();

  forward(450,385);

  setcolor(2);

  for(i=7;i<=633;i++)

    {

      line(i,46,i,423);

      delay(10);

    }

}

void win()

{ int a,b,c,i,j,x,y,fin=0;

  setcolor(6);

  rectangle(20,70,610,375);

  setfillstyle(1,0);

  floodfill(25,75,6);

  button(450,385,"Finish");

  limit(440,380,600,400);

  callmouse();

  settextstyle(7,0,8);

  while(!fin)

    {

      j=random(14)+1;

      a=random(650);

      b=random(450);

      if(a<21)

a=21;

      else if(a>609)

a=609;

      if(b<71)

b=71;

      else if(b>374)

b=374;

      for(int k=0;k<random(100);k=k+2)

{

  if(k>=(a-21))

    break;

  if(k>=(609-a))

    break;

  if(k>=(b-71))

    break;

  if(k>=(374-b))

    break;

  setcolor(j);

  circle(a,b,k);

  setcolor(15);

  outtextxy(315,222,"You Win");

  delay(5);

}

      mousepos(&c,&x,&y);

      if(c&2)

{

  rt_clk();

  do

    {

      mousepos(&c,&x,&y);

    } while(c&2);

  setfillstyle(1,2);

  floodfill(158,426,15);

}

      if(c&1)

{

  if((x>451)&&(y>385)&&(x<604)&&(y<411))

    {

      fin=1;

      reverse(450,385);

    }

  else

    {

      fin=0;

      forward(450,385);

    }

  do

    {

      mousepos(&c,&x,&y);

    } while(c&1);

}

    }

  mousehide();

  forward(450,385);

  setcolor(2);

  for(i=7;i<=633;i++)

    {

      line(i,46,i,423);

      delay(10);

    }

}

void play()

{

  int x,y,c,x1,y1,x2,y2,a,i,j,p,r,mov=1,w=0;

  char *ch;

  for(i=0;i<16;i++)

    bin[i]=0;

  loading();

  select();

  reserve();

  play_scr();

  while(mov<=10)

    {

      shuffle();

      shuffle_scr();

      res_scr();

      setfillstyle(1,10);

      floodfill(555,300,15);

      setfillstyle(1,2);

      floodfill(555,300,15);

      setfillstyle(1,6);

      floodfill(388,425,15);

      settextstyle(7,0,1);

      setcolor(14);

      sprintf(ch,"%d",mov);

      outtextxy(590,320,ch);

      outtextxy(388,445,"Select a card to exchange.");

      limit(20,300,610,400);

      callmouse();

      a=0;

      while(!a)

{

  mousepos(&c,&x,&y);

  if(c&2)

    {

      rt_clk();

      do

{

  mousepos(&c,&x,&y);

} while(c&2);

      setfillstyle(1,6);

      floodfill(158,425,15);

      settextstyle(7,0,1);

      setcolor(14);

      outtextxy(388,445,"Select a card to exchange.");

    }

  if(c&1)

    {

      if((x>451)&&(x<604)&&(y>380)&&(y<406))

{

  a=6;

  reverse(450,380);

}

      for(i=40;i<=340;i+=100)

{

  if((x>i)&&(x<(i+70)))

    {

      if((y>310)&&(y<400))

{

  j=(x-40)/100;

  x1=i;

  y1=310;

  a=1;

  break;

}

    }

}

      do

{

  mousepos(&c,&x,&y);

} while(c&1);

    }

}

      if(a==6)

{

  mousehide();

  forward(450,380);

  exit_game();

}

      mousehide();

      design_rev(x1,y1,pl[j]);

      p=j;

      limit(20,50,610,270);

      callmouse();

      setfillstyle(1,2);

      floodfill(158,425,15);

      setfillstyle(1,6);

      floodfill(158,425,15);

      settextstyle(7,0,1);

      setcolor(14);

      outtextxy(388,445,"Select a card in exchange.");

      a=0;

      while(!a)

{

  mousepos(&c,&x,&y);

  if(c&2)

    {

      rt_clk();

      do

{

  mousepos(&c,&x,&y);

} while(c&2);

      setfillstyle(1,6);

      floodfill(158,425,15);

      settextstyle(7,0,1);

      setcolor(14);

      outtextxy(388,445,"Select a card in exchange.");

    }

  if(c&1)

    {

      for(i=40;i<=540;i+=100)

{

  if((x>i)&&(x<(i+70)))

    {

      if(((y>70)&&(y<160))||((y>190)&&(y<280)))

{

  j=((x-40)/100)+(((y-70)/120)*6);

  x2=i;

  if((y>70)&&(y<160))

    y2=70;

  else

    y2=190;

  a=1;

  break;

}

    }

}

      do

{

  mousepos(&c,&x,&y);

} while(c&1);

    }

}

      mousehide();

      setcolor(15);

      rectangle(x2,y2,x2+70,y2+90);

      setfillstyle(1,4);

      floodfill(x2+5,y2+5,15);

      design(x2,y2,res[j]);

      r=j;

      a=pl[p];

      pl[p]=res[r];

      res[r]=a;

      design(x1,y1,pl[p]);

      design_bk(x2,y2);

      if(win_chk())

{

  w=1;

  break;

}

      setfillstyle(1,2);

      floodfill(388,425,15);

      mov++;

    }

  setcolor(2);

  for(i=7;i<=633;i++)

    {

      line(i,46,i,423);

      delay(10);

    }

  setfillstyle(1,2);

  floodfill(388,425,15);

  if(w==1)

    win();

  else

    loose();

  limit(10,10,620,410);

  callmouse();

}

void inst_txt()

{

  settextstyle(4,0,4);

  setcolor(6);

  outtextxy(320,65,"Instruction");

  settextstyle(4,0,2);

  outtextxy(320,95,"1) Select 4 cards from randomly placed face hidden 16 cards.");

  outtextxy(320,115,"2) The remaining 12 cards are placed face hidden.");

  outtextxy(320,135,"3) The cards choosen are to be replaced by one of");

  outtextxy(320,155,"the cards in the remaining cards section.");

  outtextxy(320,175,"4) One card is to be replaced at a time.");

  outtextxy(320,195,"5) The card replacement is termed as \"Move\".");

  outtextxy(320,215,"6) Collect four cards of same suit within 10 moves.");

  outtextxy(320,235,"7) You may also abort the game in the midway.");

}

void abt_txt()

{

  settextstyle(4,0,4);

  setcolor(6);

  outtextxy(320,65,"About Game");

  settextstyle(4,0,2);

  outtextxy(320,95,"\"Suit 16\" game comprises of 16 face cards out of");

  outtextxy(320,115,"the deck of 52 cards. The aim of the game is to");

  outtextxy(320,135,"collect 4 face cards of same suit in the maximum");

  outtextxy(320,155,"of 10 moves.");

  outtextxy(320,205,"Programmer: PRASENJIT DAS");

}

void common(int op)

{

  int ok=0,x,y,c;

  setfillstyle(1,10);

  floodfill(10,50,15);

  limit(10,50,600,410);

  button(244,390,"OK");

  switch(op)

    {

      case 2: inst_txt();

      break;

      case 3: abt_txt();

    }

  while(!ok)

    {

      mousepos(&c,&x,&y);

      if(c&2)

{

  rt_clk();

  do

    {

      mousepos(&c,&x,&y);

    } while(c&2);

  setfillstyle(1,2);

  floodfill(158,426,15);

}

      if(c&1)

{

  if((x>245)&&(y>391)&&(x<398)&&(y<416))

    {

      ok=1;

      reverse(244,390);

    }

  else

    {

      ok=0;

      forward(244,390);

    }

  do

    {

      mousepos(&c,&x,&y);

    } while(c&1);

}

    }

  forward(244,390);

  limit(10,10,620,410);

  mousehide();

  setcolor(8);

  rectangle(235,385,405,420);

  setfillstyle(1,3);

  floodfill(237,387,8);

  setfillstyle(1,2);

  floodfill(10,50,15);

  callmouse();

}

int menuclk()

{

  int i,x,y,c,op=0;

  settextstyle(7,0,1);

  setcolor(14);

  outtextxy(388,445,"Click on Menu Buttons.");

  while(!op)

    {

      mousepos(&c,&x,&y);

      if(c&2)

{

  rt_clk();

  do

    {

      mousepos(&c,&x,&y);

    } while(c&2);

  setfillstyle(1,2);

  floodfill(158,426,15);

}

      if(c&1)

{

  if((y>8)&&(y<30))

    {

      if((x>8)&&(x<161))

{

  op=1;

  reverse(7,7);

}

      else if((x>165)&&(x<318))

{

  op=2;

  reverse(164,7);

}

      else if((x>321)&&(x<474))

{

  op=3;

  reverse(320,7);

}

      else if((x>477)&&(x<630))

{

  op=4;

  reverse(476,7);

}

    }

  else

    {

      switch(op)

{

  case 1: forward(7,7);

  break;

  case 2: forward(164,7);

  break;

  case 3: forward(320,7);

  break;

  case 4: forward(476,7);

}

      op=0;

    }

  do

    {

      mousepos(&c,&x,&y);

    } while(c&1);

}

    }

  switch(op)

    {

      case 1: forward(7,7);

      play();

      break;

      case 2: forward(164,7);

      common(2);

      break;

      case 3: forward(320,7);

      common(3);

      break;

      case 4: forward(476,7);

      exit_game();

    }

  return op;

}

void screen()

{

  int clk;

  setcolor(15);

  line(6,45,634,45);

  rectangle(6,424,156,474);

  rectangle(156,424,634,474);

  button(7,7,"Play Game");

  button(164,7,"Instructions");

  button(320,7,"About Game");

  button(476,7,"Exit");

  initmouse();

  limit(10,10,620,410);

  callmouse();

  do

    {

      clk=menuclk();

    } while(clk!=4);

  closegraph();

}

void main()

{

  clrscr();

  int gd=DETECT,gm;

  initgraph(&gd,&gm,"c:\\tc\\bgi");

  getch();

  welcome();

  screen();

}