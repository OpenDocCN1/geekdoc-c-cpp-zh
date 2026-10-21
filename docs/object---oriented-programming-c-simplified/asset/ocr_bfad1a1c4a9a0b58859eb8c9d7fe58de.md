```
```cpp
{
    void show(int =20,int =30, int =40);

    clrscr( );

    show(1,2,3);
    show(1,2);
    show(1);
    show( );

    getch( );
}

void show(int p,int q,int r)
{
    cout << “Argument to show was\n”;
    cout << “p=” <<p<< “\tp=” <<q<< “\tr=” << r << endl;
}
```
```

# **OUTPUT :**

```
Argument to show was

p=1        p=2        r=3

Argument to show was

p=1        p=2        r=40

Argument to show was

p=1        p=30       r=40

Argument to show was

p=20       p=30       r=40
```

**EXPLANATION :** In the function **show** all three parameters are default. In the function call **show (1, 2, 3)** all three default parameters are overridden and **1, 2, 3** assigned to **p, q, r** respectively. In the function call **show (1, 2)** the two parameters (from left) are overridden and **r** takes default value. Similar analogy applies to rest of the **show** statements.