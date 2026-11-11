```
}
cout<<"Student grades are"<<endl;
for(int k=0;k<5;k++)
{
    if(arr[k]<40)
        goto lbl;
    else
    {
        if(arr[k]>90)
            cout<<"A grade"<<endl;
        else if(arr[k]>=70 && arr[k]<=90)
            cout<<"B grade"<<endl;
        else if(arr[k]>=40 && arr[k]<70)
            cout<<"C grade"<<endl;
    }
    lbl:if(arr[k]<40)
    {
        cout<<"Fail"<<endl;
        continue;
    }
}
return 0;
}
```

# Output:

```
Grade Show
Enter the marks of any five students
23
92
75
65
86
Student grades are
Fail
A grade
B grade
C grade
B grade
```

In Listing 27, grades of five students are shown based on the marks entered at runtime. The control of the program passes to the goto statement (lbl), if marks entered are less than 40. The statement following the goto statement gets executed and Fail gets displayed. The continue statement inside the goto statement passes the control back to the if statement to evaluate other marks. If the marks entered are greater than 90, then A grade is displayed; whereas, if marks entered are greater than 70 and less than 90, then B grade is displayed. In case, marks entered ranges between 40 and 70, then C grade is displayed.

![](bbox=[0.229, 0.809, 0.263, 0.84])

> The use of goto statements is strongly discouraged as it can make a program complex to debug by creating many different execution paths. Such a program, which has a complex control structure, is called spaghetti code.