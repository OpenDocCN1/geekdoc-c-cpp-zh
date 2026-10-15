application. To register our service for a specific component, such as the ProductListComponent, we register the service in that component like this.

```
```typescript
@Component({
  templateUrl: './product-list.component.html',
  providers: [ProductService]
})
export class ProductListComponent { }
```
```

The service is then available to the component and its child components. Note that the providedIn feature is new in Angular version 6. In older code, you'll see the service registered in a module like this.

```
```typescript
@NgModule({
  imports: [ BrowserModule ],
  declarations: [ AppComponent ],
  bootstrap: [ AppComponent ],
  providers: [ProductService]
})
export class AppModule { }
```
```

This syntax is still valid. However, the recommended practice is to use the new providedIn feature in the service instead. This provides better tree shaking. Tree shaking is a process whereby the Angular compiler shakes out unused code for smaller deployed bundles. We'll talk more about tree shaking later in this book. Now that we have registered the service, let's see how to inject the service so we can use it.