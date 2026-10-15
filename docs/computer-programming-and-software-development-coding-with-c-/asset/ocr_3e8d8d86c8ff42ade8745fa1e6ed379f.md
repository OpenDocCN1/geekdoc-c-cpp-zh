and pass in the URL to the desired server. Use generics to specify the response return type. This will transform the raw HTTP response to the specified type.

```
getProducts(): Observable<IProduct[]> {
  return this.http.get<IProduct[]>(this.productUrl).pipe(
    tap(data => console.log(JSON.stringify(data))),
    catchError(this.handleError)
  );
}

private handleError(err: HttpErrorResponse) {
}
```

Add error handling in the service as desired using the catchError operator. In any component that needs data from a data service, call the subscribe method to subscribe to the observable. Provide a function to execute when the observable emits an item.

```
ngOnInit(): void {
  this.productService.getProducts().subscribe({
    next: products => this.products = products,
    error: err => this.errorMessage = err
  });
}
```

This often assigns a property to the returned data, and if that property is bound to a template, the retrieved data appears in the view. And add an error function to handle any returned errors. The component should unsubscribe from any observable it subscribes to. Store the subscription in a variable, implement the OnDestroy lifecycle hook, and use the subscription variable in the ngOnDestroy method to unsubscribe. We have now removed the hardcoded data