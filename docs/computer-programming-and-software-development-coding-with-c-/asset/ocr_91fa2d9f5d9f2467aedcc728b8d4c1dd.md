discussion about lifecycle hooks? Earlier in this book, we said that the OnInit lifecycle hook provides a place to perform any component initialization, and it's a great place to retrieve the data for the template. Let's use the OnInit lifecycle hook. We want to set the products property to the products returned from our service. To call the service, we use our private variable containing the injected service instance, we then type a dot and the name of the method we want to call. Notice how IntelliSense helps us with all of this. There is a small problem with our code at this point.

```
ngOnInit(): void {
  this.products = this.productService.getProducts();
  this.listFilter = 'cart';
}
```

We aren't binding to the products property. We are binding to the filteredProducts property, and the filteredProducts property isn't set until a filter by string is entered. So when the application is initialized, let's set the filteredProducts property to our full list of products.

```
ngOnInit(): void {
  this.products = this.productService.getProducts();
  this.filteredProducts = this.products;
  this.listFilter = 'cart';
}
```

Let's make one more little change. Let's remove the default listFilter value, so we'll see all of the products in the list.

```
ngOnInit(): void {
  this.products = this.productService.getProducts();
  this.filteredProducts = this.products;
}
```

We should be all set to see our result in the browser, and here are our products. Notice that we have more products displayed now