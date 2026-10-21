```
cout << "str = " << str << endl;
}
void main()
{
clrscr();
third t("Welcome",10,20,34.5f);
t.show();
getch();
}
```

OUTPUT :
Con of first called
Con of second called
Con of third called
fa=10
sa=20
sb=34.5
str=Welcome

![](bbox=[0.05, 0.32, 0.95, 0.62])

# Figure 9.14. Output screen of program 9.36

When statement third t ("Welcome", 10, 20, 34.5f); executes, parameterized constructor of class third is called and ("Welcome", 10, 20, 34.5f) are passed. Inside the constructor of t they are collected in formal parameter s, x, y and z respectively. From the constructor of class third constructor of class first is called with x an assignment. In the class first this x is assigned to fa and cout displays Con of first called. Control comes back to constructor of class third which now calls constructor of class second passing parameters y and x. Inside the constructor of class second they are assigned to sa and sb and Con of second called is displayed. When control returns to constructor of class third, it enters into its body and assigns s to str and displays Con of third called.