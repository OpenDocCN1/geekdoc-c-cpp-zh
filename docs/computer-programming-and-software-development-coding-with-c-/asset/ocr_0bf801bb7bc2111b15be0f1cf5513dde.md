```
private handleError(err: HttpErrorResponse) {
  // in a real world app, we may send the server to some remote logging infrastructure
  // instead of just logging it to the console
  let errorMessage = '';
  if (err.error instanceof ErrorEvent) {
    // A client-side or network error occurred. Handle it accordingly.
    errorMessage = `An error occurred: ${err.error.message}`;
  } else {
    // The backend returned an unsuccessful response code.
    // The response body may contain clues as to what went wrong,
    errorMessage = `Server returned code: ${err.status}, error message is: ${err.message}`;
  }
  console.error(errorMessage);
  return throwError(() => errorMessage);
}
```

In this method, we handle logging our errors anyway we want. For our sample application, we'll just log to the console and throw an error to the calling code. So our getProducts method is complete. We can add other methods here to post or put data as well, but we still have that syntax error here and we can't see the result of our hard work because we are not yet subscribing to the observable.