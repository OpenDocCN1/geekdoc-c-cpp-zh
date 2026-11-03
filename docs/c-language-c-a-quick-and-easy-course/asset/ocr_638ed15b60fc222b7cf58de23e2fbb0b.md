```
long Cube(int n){return n*n*n;}
main() {int k; puts("\nType number:"); scanf("%d",&k); printf("%d",Cube(k));}
```

```
short
main() {short m; float j,k;puts("\nType two numbers:"); scanf("%f %f",&j,&k); m=fmod(j,k); printf("\nRemainder: %d",m);}
```

```
signed
main() {signed int i; puts("\n"); for(i=-20;i<=20;i+=2) printf(" %d",i);}
```

```
sizeof
main() {float a,e=2.71828; a=100*e; printf("\nValor: %f Bytes: %d",a,sizeof(float));}
```

```
static (rem.: with math.h)
main() {static float t,y;puts("\nType positive number:"); scanf("%f",&y); t=cos(3.14/6); t=log10(t); printf("\nL=%f log(cos(pi/4))=%f",log10(y),t);}
```

```
struct (rem.: with string.h)
main() {struct Cla {char mt[30];float m;}; struct Cla ja; strcpy(ja.mt,"Tue"); ja.m=5.7; printf("\nSubject: %s\nMark: %2.1f",ja.mt,ja.m);}
```

```
switch
main() {char c; puts("\nMarried?(y/n): "); c=getchar(); switch(c) {case 's': puts("Spouse.");break; case 'n': puts("Single."); break; default:puts("Error!");}}
```

```
typedef
typedef enum Boole{fals, true} Boole;
main() {Boole ini; ini=true; printf("\n Value=%d",ini);}
```

```
union
main() {union Some {char k; int i;}; asc;
```