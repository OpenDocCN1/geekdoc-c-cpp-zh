```
d3.output();
cout<<"-------------d4-------------"<<endl;
d4.output();
}
```

# Output

![](bbox=[0.26, 0.25, 0.76, 0.52])

Let us trace the output of the code from the first line of the main() function. The statement

```
Data d1(10,2.5);
```

creates an object d1 of class Data by invoking the constructor with two arguments, thereby initializing the members a and b to 10 and 2.5, respectively, as shown in the Figure 12.18. The next statement

```
Data d2(d1);
```

creates the object d2 of class Data by invoking a 'copy constructor' with passing the object d1 as an argument to the constructor. As seen, the object d1 as passed by reference, therefore the reference variable t (which is created as a formal argument to the constructor) now represents another name to the actual argument d1. Hence, we can now access the value of the member a of object d1 as t.a and the value of the member b of object d1 as t.b. This is because the reference t is just another name to object d1. Also, it is important to understand that the copy constructor is invoked by the object d2, and hence the members a and b of object d2 can be directly accessed inside the copy constructor as seen in the Figure 12.19. Therefore, the copy constructor will copy the members of object d1 into object d2, using a reference variable t as shown in the Figure 12.19. Hence, the values of the members a and b of the object d2 will also be 10 and 2.5 respectively, which are exactly same as that of the object d1.

![](bbox=[0.76, 0.72, 0.83, 0.77])

**Figure 12.18:** State of object d1