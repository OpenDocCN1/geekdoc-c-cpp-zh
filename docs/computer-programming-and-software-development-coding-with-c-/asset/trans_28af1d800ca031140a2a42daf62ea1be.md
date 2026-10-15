

首先，我们指定 Web 服务器上产品的 URL。这定义了我们发送 HTTP 请求的位置。请注意，此 URL 仅用于说明目的，并不是真实的 URL。接下来我们添加一个构造函数。回想一下，我们使用构造函数来注入依赖项。在这种情况下，我们需要 Angular 的 HTTP 服务，因此在此处注入它。由于我们将此变量强类型为 `HttpClient`，因此在此处导入 `HttpClient`。还请记住，在我们将服务作为依赖项注入之前，需要将该服务的提供程序注册到 Angular 的注入器中。HTTP 服务提供程序的注册已在 `HttpClientModule` 中为我们完成。为了将此外部包的功能包含到我们的应用程序中，我们将其添加到应用程序的 Angular 模块 `AppModule` 的 imports 数组中。回想一下，declarations 数组用于声明属于此模块的组件、指令和管道。imports 数组用于引入外部模块。我们声明我们的组件，我们声明这些组件所需的指令和管道，并导入我们需要的外部模块。回到 `product.service`，在 `getProducts` 中，我们使用注入的 HTTP 服务实例并调用 `get` 方法，传入所需的 URL。

```typescript
...
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

我们通过设置 `get` 方法的泛型参数来指定响应的预期类型。回想一下，泛型参数允许我们为此方法处理的数据定义一个类型。由于我们期望一个产品数组，因此我们将泛型参数设置为 `IProduct` 数组。`get` 方法然后自动将从服务器返回的响应映射到定义的类型，因此我们无需手动处理。我们还没有完全完成。我们的 方法现在返回什么？由于我们使用强类型，我们应该有一个函数返回值。这里我们将 `get` 方法的泛型参数定义为 `IProduct` 数组，所以我们会得到这个吗？不完全是。`http.get` 方法返回一个 observable，因此当响应从服务器返回时我们会收到通知。由于此方法返回 `http.get` 的结果，而 `http.get` 返回一个 observable，因此我们的方法返回一个 observable。由于我们告诉 `HttpClient` 服务将响应映射为产品数组，我们的 observable 会发出该产品数组。我们用泛型参数来表示这一点。因此我们的 `getProducts` 不再返回产品数组。相反，它返回一个 observable，当响应从 Web 服务器返回时，该 observable 会发出产品数组。这段代码会发送 `http.get` 请求吗？不会。你知道为什么吗？这段代码返回一个 observable，而该 observable 在我们订阅之前不会执行任何操作。

## 第 24 章 异常处理

正如你所想象的，在与服务通信时可能会出现许多问题，从无效请求到连接丢失。因此让我们添加一些异常处理。我们需要两个关键的 observable 操作符。`tap` 会接入 observable 流并允许我们在不转换流的情况下查看流中发出的值。因此 `tap` 对于调试或日志记录非常有用。

```typescript
...
import { HttpClient, HttpErrorResponse } from '@angular/common/http';
import { Observable, catchError, tap } from 'rxjs';
...

getProducts(): Observable<IProduct[]> {
  return this.http.get<IProduct[]>(this.productUrl).pipe(
    tap(data => console.log('All: ', JSON.stringify(data))),
    catchError(this.handleError)
  );
}

private handleError(err: HttpErrorResponse) {
}
```

`catchError` 会捕获任何错误。我们都从 RxJS 导入它们。正如我们在本书前面讨论的那样，要使用这些操作符，我们访问 observable 的 `pipe` 方法。然后我们传入操作符，用逗号分隔。在这里，`tap` 操作符将检索到的数据记录到控制台。这样我们可以验证它是否已正确检索。并且 `catchError` 操作符接收一个错误处理方法。错误处理方法接收一个参数，即错误响应对象。在错误处理方法中，我们可以根据需要处理错误。我们可以将错误信息发送到远程日志记录基础设施或向调用代码抛出错误。现在让我们为我们的产品服务添加异常处理。我们回到编辑器中的产品服务，就像我们离开时一样。如果没有异常处理，这段代码并不完整，因此我们将添加 `catchError` 和 `tap` 操作符的适当导入。

```typescript
import { HttpClient } from "@angular/common/http";
import { Injectable } from "@angular/core";
import { Observable, catchError, tap } from "rxjs";

import { IProduct } from "./product";

@Injectable({
  providedIn: 'root'
})
export class ProductService {
  private productUrl = 'api/products/products.json';

  constructor(private http: HttpClient) {}

  getProducts(): Observable<IProduct[]> {
    return this.http.get<IProduct[]>(this.productUrl);
  }
}
```

回想一下，HTTP GET 返回一个 observable。我们调用 observable 的 `pipe` 方法来指定一组操作符，首先是 `tap` 操作符，用于在不修改它的情况下访问发出的项目。`tap` 操作符接收一个箭头函数。参数是发出的数据，函数定义了我们想要对该数据做什么。在这种情况下，我们将其记录到控制台。这里我们使用 `JSON.stringify`。`JSON.stringify` 是一个 JavaScript 方法，它将对象或对象数组转换为 JSON 字符串。这使得在控制台中显示更容易。我们想要添加第二个操作符，因此我们插入一个逗号，然后是 `catchError` 操作符。`catchError` 也接收一个函数，但这次我们将传入一个命名函数或命名方法，而不是箭头函数。

```typescript
import { HttpClient } from "@angular/common/http";
import { Injectable } from "@angular/core";
import { Observable, catchError, tap } from "rxjs";

import { IProduct } from "./product";

@Injectable({
  providedIn: 'root'
})
export class ProductService {
  private productUrl = 'api/products/products.json';

  constructor(private http: HttpClient) {}

  getProducts(): Observable<IProduct[]> {
    return this.http.get<IProduct[]>(this.productUrl).pipe(
      tap(data => console.log('All', JSON.stringify(data))),
      catchError(this.handleError)
    );

  }
}
```

我将粘贴 `handleError` 方法，并且我们需要 `HttpErrorResponse` 和 `throwError` 的导入。

```typescript
private handleError(err: HttpErrorResponse) {
  // in a real world app, we may send the error to some remote logging infrastructure
  // instead of just logging it to the console
  let errorMessage = '';
  if (err.error instanceof ErrorEvent) {
    // A client-side or network error occurred. Handle it accordingly.
    errorMessage = `An error occurred: ${err.error.message}`;
  } else {
    // The backend returned an unsuccessful response code.
    // The response body may contain clues as to what went wrong.
    errorMessage = `Server returned code: ${err.status}, error message is: ${err.message}`;
  }
  console.error(errorMessage);
  return throwError(() => errorMessage);
}
```

在此方法中，我们可以按我们想要的方式处理错误日志记录。对于我们的示例应用程序，我们只需记录到控制台并向调用代码抛出错误。因此我们的 `getProducts` 方法已完成。我们也可以在此处添加其他方法来发布或放置数据，但我们仍然有这个语法错误，而且由于我们尚未订阅 observable，因此我们看不到我们辛苦工作的成果。

## 第 25 章 如何订阅 Observable

Observable 是惰性的。就像报纸或新闻通讯一样，observable 在我们订阅之前不会发出值。因此，当我们准备好在组件中开始接收值时，我们调用 `subscribe`。`subscribe` 方法接收一个可选参数，即 Observer 对象。顾名思义，Observer 对象观察流并响应三种类型的通知：next、error 和 complete。我们使用 Observer 对象来定义在这些通知上执行的处理函数。第一个处理函数通常称为 next 函数，因为它处理下一个发出值。由于 observable 可以随时间处理多个值，因此 nextFn 会为 observable 发出的每个值调用。第二个是错误处理函数，如果发生错误则执行。在某些情况下，我们想知道 observable 何时完成，因此 observable 提供第三个处理程序，在完成时执行。`subscribe` 函数返回订阅。我们使用该订阅来调用 `unsubscribe` 并在需要时取消订阅。

```typescript
getProducts(): Observable<IProduct[]> {
  return this.http.get<IProduct[]>(this.productUrl).pipe(
    tap(data => console.log('All: ', JSON.stringify(data))),
    catchError(this.handleError)
  );
}
```

现在我们的产品数据服务返回一个 observable，任何需要产品数据的类，例如我们的类，都可以调用我们的服务并

