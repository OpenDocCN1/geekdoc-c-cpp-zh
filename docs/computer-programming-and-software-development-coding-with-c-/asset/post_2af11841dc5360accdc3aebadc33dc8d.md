
AppModule also imports the system BrowserModule to pull in the features it needs to run this application in a browser. So this is what our AppModule currently looks like. An Angular module defines the boundary or context within which the component resolves its directives and dependencies. So when a component contains a directive, Angular looks to the components module to determine which directives are visible to that component. What does that mean for us? Well, for Angular to find the directive used in the AppComponent, the ProductListComponent must also be declared in this Angular module. This is the second step when using a component as a directive. We need to ensure that the directive is visible to any component that uses it. There are two ways to expose a directive in an Angular module. We can declare the component in the Angular module. Or if the component is already declared in another Angular module, we can import that module, similar to how we import BrowserModule here. Now let's give this a try. We are back in our sample app. We defined a selector for our ProductListComponent here so we can use it as a directive in any other component. Let's use it in the AppComponent.

```
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'pm-root',
  template: `
    <div><h1>{{pageTitle}}</h1>
      <div>My First Component</div>
    </div>
  `
})
export class AppComponent {
  pageTitle: string = 'Acme Product Management';
}
```
```

So instead of displaying My First Component, we'll display our new product list template here. Replace the div tags with Going back to the code, let's open the terminal window. If you have multiple terminal windows open, use this to select the window where the application is running. Here we see the error is not a known element.

```
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'pm-root',
  template: `
    <div><h1>{{pageTitle}}</h1>
      <pm-products></pm-products>
    </div>
  `
})
export class AppComponent {
  pageTitle: string = 'Acme Product Management';
}
```

```text
Build at: 2021-05-31T17:58:07.155Z - Hash: 40495755b6d6466aba7f6 - Time: 245ms

Error: src/app/app.component.ts:7:7 - error NG8001: 'pm-products' is not a known element:
1. If 'pm-products' is an Angular component, then verify that it is part of this module.
2. If 'pm-products' is a Web Component then add 'CUSTOM_ELEMENTS_SCHEMA' to the '@NgModule.schemas' of this component to suppress this message.

<pm-products></pm-products>
```
```

And with this error, Angular gives us a solution. If is an Angular component, and in our case it is, then verify that it is part of this

module. We didn't do step 2 and declare it in our application's Angular module. We'll open the AppModule and add ProductListComponent to the declarations array.

```
```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent,
    ProductListComponent
  ],
  imports: [
    BrowserModule
  ]
```

```

Well, we're getting a squiggly line here. That means we have an error. Any guess as to what's wrong? If you said we're missing the import, you are correct. Everything we declare must be imported.

```
```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { AppComponent } from './app.component';
import { ProductListComponent } from './products/product-list.component';

@NgModule({
  declarations: [
    AppComponent,
    ProductListComponent
  ],
  imports: [
    BrowserModule
```

```

Now that our syntax error is gone, let's try it again. There's our page. It's not complete, and it's not interactive yet, but we have the basics in place. Note that after a compile error, you may need to

refresh the browser page or restart the compiler in order to see the changes in the browser.

## Acme Product Management

![](img/0155736aec718cf18821e9f10a5d308d_81_0.png)

So we successfully used our ProductListComponent as a directive. We added the selector as the directive in the containing component's template. We declared the component to the application's Angular module. Now we are ready to power up our user interface with data binding and some Angular directives.

## Chapter 8 How to Bind with Interpolation

In Angular, binding coordinates communication between the components class and its template and often involves passing data. We can provide values from the class to the template for display, and the template raises events to pass user actions or values back to the class. The binding syntax is always defined in the template. Angular provides several types of binding, and we'll look at each of them. First, we cover interpolation. The remaining data binding techniques are covered next. The double curly braces that signify interpolation are readily recognizable. The pageTitle in this example is bound to a property in the component's class.

```
export class AppComponent {
  pageTitle: string = 'Acme Product Management';
}
```

Interpolation is a binding from the class property to the template, so the value shows up here.

```
<h1>{{pageTitle}}</h1>
```

Interpolation supports much more than simple properties. We can perform operations, such as concatenation or simple calculations. We use interpolation to insert the interpolated strings into the text between HTML elements.

```
<h1>{{pageTitle}}</h1>
```

```
{{'Title: ' + pageTitle}}
```

```
{{2*20+1}}
```

Or we can use interpolation with element property assignments as in this example.

```
<h1 innerText={{pageTitle}}></h1>
```

Here we assign the innerText property of the h1 element to a bound value. Both of these examples display the same result. The syntax between the interpolation curly braces is called a template expression. Angular evaluates that expression, using the component as the context. Angular looks to the component to obtain property values or to call methods. Angular then converts the result of the template expression to a string and assigns that string to an element or directive property. So any time we want to display data, we define a property for that data in our class and use interpolation to display that data in the template. Looking at the product list template from our sample application, we hardcoded in the pageTitle here in the heading. Binding the heading to a property in the class instead of hardcoding it in the HTML makes it easier to see and change when working on the code, and we could later retrieve this text from a file or database.

```
<div class='card'>
  <div class='card-header'>
    Product List
  </div>
  <div class='card-body'>
    <div class='row'>
      <div class='col-md-2'>Filter by:</div>
      <div class='col-md-4'>
        <input type='text' />
      </div>
    </div>
    <div class='row'>
      <div class='col-md-6'>
        <h4>Filtered by: </h4>
      </div>
    </div>
    <div class='table-responsive'>
      <table class='table'>
        <thead>
          <tr>
            <th>
              <button class='btn btn-primary'>
                Show Image
              </button>
            </th>
            <th>Product</th>
            <th>Code</th>
            <th>Available</th>

```

Let's start by adding a property in the class for the pageTitle. We'll open the component to the right and close down the explorer. Here in the class, we specify the property name.

```
```html
<div class="card">
  <div class="card-header">
    Product List
  </div>
  <div class="card-body">
    <div class="row">
      <div class="col-md-2">Filter by:</div>
      <div class="col-md-4">
        <input type="text" />
      </div>
    </div>
    <div class="row">
      <div class="col-md-6">
        <h4>Filtered by: </h4>
      </div>
    </div>
    <div class="table-responsive">
      <table class="table">
        <thead>
          <tr>
            <th>
              <button class="btn btn-primary">
                Show Image
              </button>
            </th>
            <th>Product</th>
            <th>Code</th>
            <th>Available</th>
          </tr>
        </thead>
      </table>
    </div>
  </div>
</div>
```
```

```
```typescript
import { Component } from "@angular/core";

@Component({
  selector: 'pm-products',
  templateUrl: './product-list.component.html'
})
export class ProductListComponent {
}
```
```

We'll call it pageTitle. And because we are using TypeScript, we define the type for this property. Lastly, we assign a default value, Product List.

```
```typescript
import { Component } from "@angular/core";

@Component({
  selector: 'pm-products',
  templateUrl: './product-list.component.html'
})
export class ProductListComponent {
  pageTitle: string = 'Product List';
}
```
```

With the pageTitle property in place, we can now bind to the pageTitle property in the template. We replace the hardcoded product list here with interpolation and specify the name of the property. Now when this template is displayed, Angular assigns the string value of the pageTitle property to the innerText property of this div element. And Product List will be displayed.
