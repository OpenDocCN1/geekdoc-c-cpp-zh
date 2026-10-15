```
```typescript
ngOnInit(): void {
  this.productService.getProducts().subscribe({
    next: products => this.products = products,
    error: err => this.errorMessage = err
  });
}
```
```

This line of code calls the product data service getProducts method, and because we subscribed, it kicks off the HTTP get request. It then asynchronously receives data and notifications from the observable. We pass an Observer object to the subscribe. This syntax defines a key and value pair, where the key is the function name and the value is the function, specified here using arrow function syntax. The first Observer function specifies the action to take whenever the observable emits an item. The method parameter is that emitted item. Since HTTP calls are single async operations, only one item is emitted, which is the HTTP response object that was mapped to our product array in the service. So the parameter is our array of products. This code then sets the local products property to the returned array of products. The second function is executed if the observable fails. In this example, it sets a local error message variable to the returned error. A third function, not used here, specifies the action to take when the observable ends with a completed notification. The third function is rarely used when working with HTTP requests, since they automatically complete after emitting the single response. It's good practice to always unsubscribe from any observable we subscribe to. There are several ways to