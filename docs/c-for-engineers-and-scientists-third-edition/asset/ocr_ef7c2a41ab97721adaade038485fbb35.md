# Chapter 12 691

Passing Addresses

In contrast to passing addresses with references, addresses can be explicitly passed with pointers. To explicitly pass an address to a function, all you need to place the address operator, & in front of the variable being passed. For example, this function call swap(&firstnum, &secnum);

passes the addresses of the variables firstnum and secnum to swap(), as shown in Figure 12.17. Explicitly passing addresses with the address operator is also referred to as a pass by reference because the called function can reference, or access, variables in the function by using the passed addresses. As you see in Section 6.3, by references can also be made with references. In this section, you use the addresses passed with pointers to directly access the variables firstnum and secnum from swap() and exchange their values—procedure accomplished in Program 6.8 with reference parameters.

Variable name: firstnum
Variable address: an address

![](bbox=[0.255, 0.378, 0.765, 0.513])

Figure 12.17 Explicitly passing addresses to swap()

One of the first requirements in writing swap() is to construct a function header that receives and stores the passed values, in which case are two addresses. As you see in Section 12.1, addresses are stored in pointers, which means the parameters of swap() must be declared as pointers.

Assuming firstnum and secnum are double-precision variables and swap() returns no value, a suitable function header for swap() is as follows:

```
void swap(double *nm1Addr, double *nm2Addr);
```

The choice of the parameter names nm1Addr and nm2Addr is, with all parameters, up to the programmer. The declaration double *nm1Addr, however, states that the parameter named nm1Addr is used to store the address of a double-precision value. Similarly, the declaration double *nm2Addr specifies that nm2Addr also stores the address of a double-precision value.

Before the body of swap() to exchange the values in firstnum and secnum, first check that the values accessed by using the addresses in nm1Addr and nm2Addr are correct. Program 12.10 performs this check.

The output displayed when Program 12.10 runs as follows:

The number whose address is in nm1Addr is 20.5
The number whose address is in nm2Addr is 6.25