```
capitalizeName(product: IProduct): string {
  return product.productName.toUpperCase();
}
```

To write this code as an arrow function, we ignore the function name, as arrow functions don't need a name to find the parameters, then an arrow.

```
(product: IProduct) => product.productName.toUpperCase();
```

This is what gives an arrow function its name. We ignore the curly braces and return keyword. Arrow functions with a single statement have an implied body and return. Then we write the required logic. If the arrow function requires multiple statements in the function body, then we do need to use curly braces and the return keyword.

```
(product: IProduct) => {
  console.log(product.productName);
  return product.productName.toUpperCase();
}
```

Use an arrow function any time you need to pass a function into another function or method. We'll see more arrow functions later in this book.

```
performFilter(): IProduct[] {
  return this.products.filter((product: IProduct) =>
    product.productName.includes(this.listFilter));
}
```