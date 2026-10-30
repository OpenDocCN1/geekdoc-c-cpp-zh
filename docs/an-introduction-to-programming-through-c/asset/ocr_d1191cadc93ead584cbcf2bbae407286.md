This may be called using the following main program.

```
main(){
    char a[40], b[40];
    cin.getline(a,40);
    cin.getline(b,40);
    cout << a << " " << compare(a,b) << " " << b << endl;
}
```

If you execute this program, it would expect you to type two lines. Say you typed:

```
Mathematics
Biology
```

then it would print out > and stop, because “Mathematics” appears after “Biology” in the dictionary order.

# 14.1.4 Address arithmetic

C++ programs processing char arrays often use arithmetic on addresses.

Suppose x is the name of an array of some type T. We have already said that x has value equal to the address of the zeroth element of the array. Suppose further that i is an integer expression. Then the expression

```
x+i
```

is valid in C++ programs, and has the value equal to the address of x[i]. Note that in general, a single element of type T may require some s bytes. Thus while x+i seems to be adding i to the address x, the actual value added is i*s because the address of x[0] and of x[i] differ by i*s and not just i. Indeed, in general, if x is of type T*, then x+i is the address obtained by adding i*s to the address denoted by x. Since this can be somewhat confusing, we have not discussed such address arithmetic so far.

However, if x is of type char*, then s equals 1. In that case, when we write x+i, we indeed mean the address obtained by adding i. So perhaps for this reason, address arithmetic is quite common in character processing. Thus the scopy function would more commonly be written as:

```
void scopy(char *destination, char *source){
    while(*source != '\0'){
        *destination = *source;
        destination++;
        source++;
    }
}
```