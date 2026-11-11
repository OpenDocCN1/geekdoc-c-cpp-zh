```
```c
printf("\nInput increment values:");
printf("    price increment and quantity increment\n");
scanf("%f %d", &p_increment, &q_increment);

/* - - - - - - - - - - - - - - - - - - - - - - */
item = update(item, p_increment, q_increment);
/* - - - - - - - - - - - - - - - - - - - - - - */
printf("Updated values of item\n\n");
printf("Name        : %s\n",item.name);
printf("Price       : %f\n",item.price);
printf("Quantity    : %d\n",item.quantity);

/* - - - - - - - - - - - - - - - - - - - - - - */
value = mul(item);
/* - - - - - - - - - - - - - - - - - - - - - - */

printf("\nValue of the item  = %f\n", value);
}
struct stores update(struct stores product, float p, int q)
{
    product.price += p;
    product.quantity += q;
    return(product);
}
float mul(struct stores stock)
{
    return(stock.price * stock.quantity);
}
```
```

# Output

```
Input increment values:    price increment and quantity increment
10 12
Updated values of item
Name     : XYZ
Price    : 35.750000
Quantity : 24
Value of the item = 858.000000
```

**Fig. 12.6**  *Using structure as a function parameter*

You may notice that the template of **stores** is defined before **main()**. This has made the data type **struct stores** as *global* and has enabled the functions **update** and **mul** to make use of this definition.