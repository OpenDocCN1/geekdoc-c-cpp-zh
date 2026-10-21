```
ptr->display();
ptr->fun();
ptr = &s;
ptr->show();
ptr->display();
ptr->fun();
ptr = &t;
ptr->show();
ptr->display();
ptr->fun();
getch();
}
```

OUTPUT :
Hello from show of first class
Hello from display of first class
Hello from fun of first
Hello from show of second class
Hello from display of first class
Hello from fun of first
Hello from show of first class
Hello from display of third class
Hello from fun of first

EXPLANATION : The explanation is based on the basis of VPTR and VTABLE. The function show and display is virtual in class first and fun is not virtual. The class second only overrides fun and show. The class third overrides display and fun. The VTABLE for all three classes is as shown below. Note the addresses of different functions in the VTABLE. The VTABLE for the class first need no explanation. The class second overrides virtual function show but does not override display so in the VTABLE for second class address of show of second class and address of display of first class is put. Similarly for the VTABLE of class third address of show of first class and address of display of third class is put. For all three VTABLE a separate VPTR is present.

In the code shown above when ptr contains the address of object f, compiler from the contents of ptr, find out the addresses of VPTR of class first and functions of class first are called.

![](bbox=[0.28, 0.77, 0.72, 0.82])

When ptr contains the address of object s, compiler from the contents of ptr, find out the address of VPTR of class second and function from VTABLE of second gets called.