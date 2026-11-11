![](bbox=[0.303, 0.145, 0.699, 0.306])

Fig. 11.5  *One-way data communication*

We shall modify the definition of both the called functions to include arguments as follows:

**void printline(char ch)**

**void value(float p, float r, int n)**

The arguments **ch, p, r,** and **n** are called the *formal arguments*. The calling function can now send values to these arguments using function calls containing appropriate arguments. For example, the function call

**value(500,0.12,5)**

would send the values 500, 0.12 and 5 to the function

**void value( float p, float r, int n)**

and assign 500 to **p**, 0.12 to **r** and 5 to **n**. The values 500, 0.12, and 5 are the *actual arguments*, which become the values of the *formal arguments* inside the called function.

The *actual* and *formal* arguments should match in number, type, and order. The values of actual arguments are assigned to the formal arguments on a *one to one* basis, starting with the first argument as shown in Fig. 11.6.

![](bbox=[0.35, 0.568, 0.735, 0.833])

Fig. 11.6  *Arguments matching between the function call and the called function*