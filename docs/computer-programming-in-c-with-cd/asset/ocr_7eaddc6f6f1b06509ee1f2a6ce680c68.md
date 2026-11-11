# Returning Structure from Function

So far you learned to pass a structure variable as an argument to the function. Using this argument, you can change the values of the variables defined in the structure. Now, suppose you want to access these values outside the function body. For this, you have to return a structure variable by using the `return` keyword at the end of a function body to the caller functions. When a function returns a structure variable, it must match with the return type of the structure, which is declared in the function body.

Now extend the example shown in Listing 4 to return the object of the structure from the function. Listing 5 shows the input() function that returns the structure variable new_product of the product structure (you can find the ReturnStructure.cpp file on the CD in the code\chapter5 folder):

# Listing 5: Returning Structure from a Function

```
```cpp
#include <iostream.h>
#include <stdio.h>

struct product
{
    char product_number[15];
    char product_name[30];
    int product_quantity;
    float product_price;
};

product input()
{
    product new_product;
    cout<<"Enter product number :"<<endl;
    gets(new_product.product_number);
    cout<<"Enter product name :"<<endl;
    gets(new_product.product_name);
    cout<<"Enter product quantity :"<<endl;
    cin>>new_product.product_quantity;
    cout<<"Enter product price of one quantity: "<<endl;
    cin>>new_product.product_price;
    return new_product;
}

void display(product p)
{
    cout<<"The descriptions of product are -->"<<endl;
    cout<<"---------------------------------------"<<endl;
    cout<<"Product number :"<<p.product_number<<endl;
    cout<<"Product name :"<<p.product_name<<endl;
    cout<<"Product quantity :"<<p.product_quantity<<endl;
    cout<<"Product price :"<<p.product_price<<endl;
    cout<<"---------------------------------------"<<endl;
```
```