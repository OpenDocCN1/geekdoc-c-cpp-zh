```
catch(hmeanxcp& e)
{
  cout<<e.getError()<<endl;
  cout<<"Enter a fresh pair of numbers\n";
  continue;
}
catch(gmeanxcp& e)
{
  cout<<e.getError()<<endl;
  cout<<"Enter a fresh pair of numbers\n";
  continue;
}
cout<<"Harmonic mean = "<<z1<<endl;
cout<<"Geometric mean = "<<z2<<endl;
cout<<"Enter again ? "<<choice<< (y/n)<<\n";
cin>>choice;
}
cout<<"Bye\n";
```

```
double hmean(double a,double b)
{
  if(a==-b)
    throw hmeanxcp("Exception error - a=-b not allowed");
  return 2.0*a*b/(a+b);
}
double gmean(double a,double b)
{
  if(a*b<0)
    throw gmeanxcp("Exception error - a*b<0 not allowed");
  return sqrt(a*b);
}
```

# Output

Enter a number: 10<enter>
Enter another number: -10<enter>
Exception error - a=-b not allowed
Enter a fresh pair of numbers
Enter a number: 10<enter>
Enter another number: -6<enter>
Exception error - a*b<0 not allowed
Enter a fresh pair of numbers
Enter a number: 16<enter>
Enter another number: 4<enter>
Harmonic mean = 6.4
Geometric mean = 8
Enterter again? (y/n) n<enter>
Bye

A temporary copy of the object to be thrown is created and thrown. Hence, the object in the catch handler refers to a copy of the thrown object. This is desirable because the thrown object disappears after the function from which it was thrown. Thus, after the object is thrown, its three copies may be created—itself, and the object in the catch block. The object itself gets destroyed automatically when the function terminates.