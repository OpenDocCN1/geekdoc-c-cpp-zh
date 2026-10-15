# CHAPTER 25 HOW TO SUBSCRIBE TO AN OBSERVABLE

Observables are lazy. Just like a newspaper or a newsletter, an observable doesn't emit values until we subscribe. So when we are ready to start receiving values in our component, we call subscribe. The subscribe method takes an optional argument, which is an Observer object. As its name suggests, the Observer object observes the stream and responds to three types of notifications, next, error, and complete. We use the Observer object to define handler functions that execute on these notifications. The first handler function is often called a next function because it processes the next emitted value. Since observables can handle multiple values over time, the nextFn is called for each value the observable emits. The second is an error handler function, and it executes if there is an error. In some cases, we want to know when the observable completes, so observables provide a third handler that is executed on completion. The subscribe function returns the subscription. We use that subscription to call unsubscribe and cancel the subscription if needed.

```
getProducts(): Observable<IProduct[]> {
  return this.http.get<IProduct[]>(this.productUrl).pipe(
    tap(data => console.log('All: ', JSON.stringify(data))),
    catchError(this.handleError)
  );
}
```

Now that our product data service is returning an observable, any class that needs product data, such as our can call our service and