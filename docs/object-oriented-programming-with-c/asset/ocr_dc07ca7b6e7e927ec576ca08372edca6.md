```
```
*ptr; cout<< "\n"; ptr++;
cout<<"\nValue of ptr++ : "<< *ptr;
cout << "\n";
ptr--;
cout<<"\nValue of ptr-- : "<< *ptr;
cout << "\n";
ptr=ptr+2;
cout<<"\nValue of ptr+2 : "<< *ptr;
cout << "\n";
ptr-ptr-1;
cout <<"\nValue of ptr-1: "<< *ptr;
cout << "\n";
ptr+-=3;
cout<<"\nValue of ptr+=3: "<< *ptr;
ptr--;
cout << "\n";
cout<<"\nValue of ptr-=2: "<< *ptr;
cout << " \n";
getch( );
}
```
```

The output of Program 9.3 would be:

+   The array values are:
+   56
+   75
+   22
+   18
+   90
+   Value of ptr : 56
+   Value of ptr++ : 75
+   Value of ptr-- : 56
+   Value of ptr+2 : 22
+   Value of ptr-1 : 75
+   Value of ptr+-3 : 90
+   Value of ptr--2 : 22