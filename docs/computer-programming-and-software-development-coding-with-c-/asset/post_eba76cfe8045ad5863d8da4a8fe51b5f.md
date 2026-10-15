
## Chapter 21 Observables and Reactive Extensions

The data for our application is on a server somewhere, in the cloud or at the office. How do we get that data into our view? Well, in this chapter we learn how to use HTTP with observables to retrieve data. Most Angular applications obtain data using HTTP. The application issues an HTTP GET request to a web service. That web service retrieves the data, often using a database, and returns it to the application in an HTTP response. The application then processes that data.

We begin with an introduction to observables and the reactive extensions. We then examine how to send an HTTP request and map the result to an array. We add some exception handling, and we look at how to subscribe to observables to get the data for our view. We finished the first cut of a product data service, but it still has hardcoded data. We'll replace that hardcoded data with HTTP calls.

To understand the HTTP code we're about to write, it's important to understand the basics of Reactive Extensions and Observables. So let's get technical for just a moment, and then we'll break down what all of this means.

Reactive Extensions for JavaScript, or RxJS, is a library for composing data using Observable sequences, and transforming that data using a set of operators. If you are familiar with .NET, these are similar to LINQ operators. Angular uses Reactive Extensions for working with data, especially asynchronous data such as HTTP requests, which is why we're covering it here.

So what does all of this mean? Let's start with asynchronous, then cover Observable sequences, and operators.

Synchronous communication is like a phone call. It's: you talk, I immediately process the information, and respond. With synchronous data, the application requests a value and waits for it to arrive, like calling our getProducts method to get the list of products.

Asynchronous communication doesn't expect an immediate response. When I send an email, I don't have to wait for a reply. I can do something else. When I am notified of a reply sometime later, I can decide when to process it. From our application's point of view, HTTP requests are asynchronous. Here is an application and here is a web server. The application wants to display products, so we send a request to the web server, asking for the product data. We then set up to be notified when the data is returned, and continue along. At some later point in time, HTTP returns a response with the requested products, and our application notifies us that the products were returned. So this process of request and response is asynchronous. We submit a request, don't wait for it, and sometime later, receive a response.

In Angular, we issue the get request using HTTP, but what do we use to set up the notifications? That's where RxJS Observable sequences come in. An Observable sequence, sometimes called an Observable stream, or just an Observable, is a collection of items over time. So it's a collection, but unlike an array, it doesn't retain items. Rather, the emitted items can be observed over time. For example, here is an array of letters. We can traverse through the letters, sort the letters, or ask for the third letter. An Observable is more like this, letters arriving over time. We can't loop through them, sort them, or ask for the third letter after it's already been emitted. Think of these letters as mouse moves, or button clicks, or the user typing characters. The moves or clicks or key presses occur over time.

What does an Observable do? An Observable doesn't do anything until we subscribe. Think of a subscription like a streaming service. Until you subscribe, you won't get the latest movie series. When we subscribe, the Observable begins emitting notifications.

There are three types of notifications. The most common is the next notification, which occurs when the next item is emitted, and it provides the emitted item. For example, think of tracking key presses. Each time a key is pressed, the Observable emits a next notification, and provides the pressed character. If an error occurs, the Observable emits an error notification, and provides the error information. The Observable then completes, and no more items are emitted. If there are no more items to emit, the Observable emits a complete notification. Once subscribed, an Observable emits next, error, or complete notifications.

With that knowledge, let's revisit our prior chapter with a bit more detail. To get product data for display, the code calls http.get(). Http.get() returns an Observable, which will emit notifications, so we'll know when the response arrives. We then subscribe to start the Observable, and the get request is sent. Recall that Observables don't do anything until we subscribe. The code doesn't wait for the response; it just continues along. At some later point in time, the server returns a response. The Observable emits a next notification, letting us know we have the data. We can then process the emitted response. Note that when using http.get(), the Observable emits the entire response as one emitted item. So if we ask for products, the HTTP response includes the products, and the

## Chapter 22 How to Use Observable

A common way to use observables in an Angular application is to first start the observable with a subscribe, then pipe each emitted item through a set of operators to modify or transform the item. Then we process the notifications from the observable. Recall the three notifications that an observable emits? Next, error, and complete. And lastly, we stop the observable by unsubscribing.

Here is some sample code to help solidify these concepts. Observable operators and methods we can use to create observables can be found in the rxjs package.

```
import { Observable, range, map, filter } from 'rxjs';

const source$: Observable<number> = range(0, 10);

source$.pipe(
    map(x => x * 3),
    filter(x => x % 2 === 0)
).subscribe(x => console.log(x));
```

We use the observable creation function called range to create an observable that emits 10 numbers, starting from 0, so we'll have some data to work with. We use the generic argument here to define the type of data that this observable will emit. By convention, we add a dollar suffix to variables that reference an observable. This makes it easier to quickly distinguish the observables.

We use the pipe method to pipe the emitted items through several operators. In this example, map and filter. We only include two operators here, but we can define any number of operators separated by commas.

The map operator allows us to transform each emitted item. We define the logic for the transformation using an arrow function. The arrow function parameter is the emitted item. In this example, each emitted number is multiplied by 3 and then passed on to the following operator.

The filter operator decides which items to pass on and which to filter out. We define the logic for the filtering using an arrow function. The parameter to the arrow function is the item emitted from the prior operator. In this example, we filter the result to only the even numbers in the sequence, that is, those numbers, when divided by 2, have a remainder of 0.

Recall how to start the observable? We call the subscribe method. The observable then emits the range of numbers. We use an arrow function to define what we want to do with each item emitted from the pipeline. Here we simply log it. We'll talk more about the subscribe syntax and how to unsubscribe later on.

What do you think will be logged to the console? The source emits 0. The 0 is multiplied by 3, resulting in 0. The 0 is divided by 2 with a remainder of 0, so it is included in the final result. The source emits 1, the 1 is multiplied by 3, resulting in 3. The 3 is divided by 2 with a remainder of 1, so it is not included in the final result, and so on.

## Chapter 23 How to Setup an HTTP Request

We often encapsulate the data access for our application into a data service that can be used by any component or other service that needs it. We did just that, but our product data service still contains a hardcoded list of products. We instead want to send an HTTP request to get the products from a web server.

Angular provides an HTTP service that allows us to communicate with a web server using the familiar HTTP request and response protocol. For example, we call the get method of the HttpClient service, which returns an observable. When we subscribe to that observable, the HttpClient service sends a get request to the web server. The web server response is returned to the HttpClient service, and the observable emits the next notification, providing the response.

What does this look like in code? This is the ProductService we built before.

```
import { HttpClient } from '@angular/common/http';

@Injectable({
  providedIn: 'root'
})
export class ProductService {
  private productUrl = 'www.myWebService.com/api/products';

  constructor(private http: HttpClient) { }

  getProducts() {
    return this.http.get(this.productUrl);
  }
}
```
