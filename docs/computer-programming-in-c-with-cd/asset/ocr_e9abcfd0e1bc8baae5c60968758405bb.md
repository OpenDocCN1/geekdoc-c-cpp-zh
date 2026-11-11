```
cout<<"------------------------------------------"<<endl;
cout<<"Product number :"<<p.product_number<<endl;
cout<<"Product name :"<<p.product_name<<endl;
cout<<"Product quantity :"<<p.product_quantity<<endl;
cout<<"Product price :"<<p.product_price<<endl;
cout<<"------------------------------------------"<<endl;
cout<<"Total price = "<<p.product_quantity*p.product_price;
}

int main()
{
    product p;
    cout<<"Enter product number :"<<endl;
    gets(p.product_number);
    cout<<"Enter product name :"<<endl;
    gets(p.product_name);
    cout<<"Enter product quantity :"<<endl;
    cin>>p.product_quantity;
    cout<<"Enter product price of one quantity: "<<endl;
    cin>>p.product_price;
    display(p);
    return 0;
}
```

# Output:

```
Enter product number :
101
Enter product name :
Milk
Enter product quantity :
25
Enter product price of one quantity:
30
The descriptions of product are -->
------------------------------------------
Product number :101
Product name :Milk
Product quantity :25
Product price :30
------------------------------------------
Total price = 750
```

In Listing 4, a structure product is declared. The variables of this structure are accessed and assigned certain values inside the main() function. These values are displayed using the display function that takes the object of the product structure, as an argument. In this, p is the object of the structure product, which is used as an actual argument while calling display(p) function in the main() function and used as a formal argument (product p) while defining the display() function.