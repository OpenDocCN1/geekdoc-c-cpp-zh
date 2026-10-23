
The standard "printf" function that prints the output onto the screen uses the symbol "%c" to denote a variable of type character. Here is the entire implementation of the "fix()" function:

```
int fix(char* s, int length, int task){
    for(int i=length-1;i>=0;i--)
        if((s[i]=='+')||(s[i]=='-')){
            char s1[i+1];
            char s2[length-i];
            copy(s1,s,i);                 /* create first substring */
            copy(s2,s+i+1,length-i-1);/* create second substring */
            if(task==2){ /*calculate the arithmetic expression*/
                if(s[i]=='+')
                    return fix(s1,i,task) + fix(s2,length-i-1,task);
                else
                    return fix(s1,i,task) - fix(s2,length-i-1,task);
            }
            if(task==0)printf("%c",s[i]);   /* print symbol (postfix) */
            fix(s1,i,task);     /* recursive call (first substring) */
            fix(s2,length-i-1,task);/*recursive call (second substring)*/
            if(task==1)printf("%c",s[i]);   /* print symbol (prefix) */
            return 0;
        }
```

In the above loop, the string is scanned in the reverse order, and we look for the '+' or '-' character. These characters correspond to arithmetic operations of the least priority, and hence are considered first. If a '+' or '-' character is found, then the string is split into two substrings that are added or subtracted (if the task is to calculate) or printed in the postfix or prefix form (if the task is to do so). The next loop does the same for the '%' character, which stands for the modulus operation, which is of the next higher priority:

```
for(int i=length-1;i>=0;i--)
    if(s[i]=='%'){
        char s1[i+1];
        char s2[length-i];
        copy(s1,s,i);                 /* create the first substring */
        copy(s2,s+i+1,length-i-1);/* create the second substring */
        if(task==2)return fix(s1,i,task) % fix(s2,length-i-1,task);
        if(task==0)printf("%c",s[i]);/* "mod" symbol (postfix) */
        fix(s1,i,task);     /* recursive call (first substring) */
        fix(s2,length-i-1,task);/*recursive call (second substring)*/
        if(task==1)printf("%c",s[i]);/* "mod" symbol (prefix) */
        return 0;
    }
```

The next loop does the same for the '*' (or '/') character, which corresponds to multiplication (or division), which is of the highest priority, and hence is considered last:

```
for(int i=length-1;i>=0;i--)
    if((s[i]=='*')||(s[i]=='/')){
        char s1[i+1];
        char s2[length-i];
        copy(s1,s,i);            /* create first substring */
        copy(s2,s+i+1,length-i-1);/* create second substring */
        if(task==2){  /* calculate arithmetic expression */
            if(s[i]=='*')
                return fix(s1,i,task) * fix(s2,length-i-1,task);
            else
                return fix(s1,i,task) / fix(s2,length-i-1,task);
        }
        if(task==0)printf("%c",s[i]);  /* print symbol (postfix) */
        fix(s1,i,task);     /* recursive call (first substring) */
        fix(s2,length-i-1,task);/*recursive call (second substring)*/
        if(task==1)printf("%c",s[i]);  /* print symbol (prefix) */
        return 0;
    }
```

(Alternatively, the substrings "s1" and "s2" could probably be embedded in the original string 's', to avoid forming them explicitly and to increase efficiency.) Finally, the string is scanned once again, and this time we look for digits. If these are found, then the value of the integer number they form is calculated (if this is the required task) or printed to the screen (if this is the required task):

```
if(*s == '\n'){
    printf("error");
    return 0;
}
if(task==2){  /* calculation of an integer number */
    int sum=0;
    int exp=1;
    for(int i=length-1;i>=0;i--){
        if((s[i]>='0')&&(s[i]<='9')){
            sum += (s[i]-'0') * exp;
            exp *= 10;
        }
        else{
            printf("error");
            return 0;
        }
    }
    return sum;
}
for(int i=0;i<length;i++){  /* print an integer number */
    if((s[i]>='0')&&(s[i]<='9'))
        printf("%c",s[i]);
    else{

```
```
printf("error");
    return 0;
}
}
    return 0;
} /* calculate or print in prefix/postfix format */
```

This completes the "fix()" function that carries out the required task. Here is the "main()" function that actually reads the arithmetic expression (using the standard "getchar()" function to read each individual character) and carries out the three required tasks: printing it in prefix and postfix formats and calculating its value.

```
int main(){
    char s[80];
    int i;
    for(i=0; (s[i]=getchar()) != '\n'; i++);/*read expression*/
```

This loop (with empty body) reads the entire arithmetic expression character by character from the screen into the string `s` and sets the integer `i` to the number of characters that have been read. The function "fix()" can now be applied:

```
fix(s,i,0);            /* print in postfix form */
printf("\n");
fix(s,i,1);            /* print in prefix form */
printf("\n");
printf("%d\n",fix(s,i,2));   /* print expression value */
return 0;
}
```

As mentioned above, a variable that is defined inside the block of a function (local variable) is destroyed when the function ends. Still, it may be saved by declaring it as "static". For example, if we wrote in the above "fix()" function

```
static FILE* fp = fopen("writeFile","w");
fprintf(fp,"length of subexpression=%d\n",length);
```

then the length of the original arithmetic expression and the subsequent subexpressions would be printed to the file "writeFile". Here, "fp" is a pointer-to-static-file variable. This file is created and initialized the first time the function starts and exists even after it terminates. Thus, writing to the file can continue in further recursive calls to the function.

## 1.22 Example: The Exponent Function

In this section, we implement the exponent function exp(x) (also denoted by e^x). Although this function is available in the standard "math.h" library, we implement it here explicitly as a good exercise in using loops. Furthermore, the present implementation can be extended to compute the exponent of a square matrix (Chapter 2, Section 22).

The exponent function is defined as an infinite series:

```
exp(x) = 1 + x + x^2/2! + x^3/3! + ... = sum_{n=0}^{∞} x^n / n!
```

This is also the Taylor expansion (Section 5.11 below) of the exponent function around zero. We approximate this function by the truncated series

$T_K(x) = \sum_{n=0}^{K} \frac{x^n}{n!}$.

Here, $K$ is some predetermined integer, say $K = 10$.

The Taylor polynomial $T_K$ is a good approximation to the exponent function when $x$ is rather small in magnitude. When $x$ is large in magnitude, $\exp(x)$ can still be approximated by picking a sufficiently large integer $m$ in such a way that $x / 2^m$ is sufficiently small in magnitude and approximating

$\exp(x) = \exp(x / 2^m)^{2^m}$

by

$\exp(x) \doteq T_K(x / 2^m)^{2^m}$.

This formula is followed in the function "expTaylor()":

```
double expTaylor(double arg) {
    const int K=10;
    double x=arg;
}
```

First, one needs to find an appropriate integer $m$. This is done in a loop in which $x$ is successively divided by 2 until its magnitude is sufficiently small, say smaller than 0.5. The total number of times $x$ has been divided by 2 is the value assigned to $m$:

```
int m=0;
while(abs(x)>0.5) {
    x /= 2.;
    m++;
}
```

Now, we return to the evaluation of the Taylor polynomial $T_K(x)$. This can be done most efficiently in the spirit of Horner’s algorithm (Chapter 5, Section 11):

$T_K(x) = \left( \cdots \left( \left( \frac{x}{K} + 1 \right) \frac{x}{K-1} + 1 \right) \frac{x}{K-2} + 1 \cdots \right) x + 1.$

This calculation uses a loop with a decreasing index $n$ in which $T_K$ takes the initial value 1 before being successively multiplied by $x / n$ and incremented by 1:

```
double sum=1.;
for(int n=K; n>0; n--) {
    sum *= x/n;
    sum += 1.;
}
```

At this stage, the local variable "sum" has the value $T_K(x / 2^m)$. The required output, the $2^m$-power of $T_K(x / 2^m)$, is obtained from a third loop of length $m$, in which "sum" is successively replaced by its square:
