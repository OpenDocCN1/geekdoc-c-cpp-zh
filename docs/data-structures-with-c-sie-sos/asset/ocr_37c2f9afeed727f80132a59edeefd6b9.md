```
("His favorite subject was DS"),
("He was good in string handling"));
int COUNT(char[][80],int,int);
char* SUBSTR(char*,int,int);
```

```
void main()
{
int NUM,N;
clrscr();
NUM=0;
N=6;
printf("The number of instances of WORD in short story S are
%d",COUNT(S,N,NUM));
getch();
}
```

```
int COUNT(char S1[][80],int N1,int NUM1)
{
int K;
int i,J;
char BEG[10]=("THE ");
char END[10]=(" THE");
char MID[10]=(" THE ");
char TEMP[80];
K=0;
while(K<N1)
{
i=0;
while(S1[K][i]!='\0')
{
TEMP[i]=S1[K][i];
i=i+1;
}
TEMP[i]='\0';
if(strcmp(SUBSTR(TEMP,1,4),BEG)==0)
NUM1=NUM1+1;
if(strcmp(SUBSTR(TEMP,strlen(TEMP)-3,4),END)==0)
NUM1=NUM1+1;
for(J=2;J<strlen(TEMP)-5;J++)
if(strcmp(SUBSTR(TEMP,J,5),MID)==0)
NUM1=NUM1+1;
```