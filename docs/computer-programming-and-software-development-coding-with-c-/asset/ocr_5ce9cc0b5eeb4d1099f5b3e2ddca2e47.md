then add ConvertToSpacesPipe to the declarations and add the needed import.

```
<> product-list.component.html
TS app.module.ts ×
TS convert-to-spaces.pipe.ts
1  import { BrowserModule } from '@angular/platform-browser';
2  import { NgModule } from '@angular/core';
3  import { FormsModule } from '@angular/forms';
4
5  import { AppComponent } from './app.component';
6  import { ProductListComponent } from './products/product-list.component';
7  import { ConvertToSpacesPipe } from './shared/convert-to-spaces.pipe';
8
9  @NgModule({
10    declarations: [
11      AppComponent,
12      ProductListComponent,
13      ConvertToSpacesPipe
14    ],
15    imports: [
16      BrowserModule,
17      FormsModule
18    ],
19    bootstrap: [AppComponent]
20  })
21  export class AppModule { }
```

Now any component declared in AppModule can use the ConvertToSpacesPipe. Our product code now appears with spaces instead of dashes. Build a custom pipe anytime you need to perform data transformations. Notice, however, that our page interactivity is still not complete. The product list is not yet filtering based on the filter criteria. Let's look at that next. We have an input box here for the user to enter a filtered string. The list of products should then be filtered on the entered string.