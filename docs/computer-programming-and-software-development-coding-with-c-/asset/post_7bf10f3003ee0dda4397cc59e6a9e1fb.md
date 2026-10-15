
We'll focus on building a nested component. So what makes a component nestable? Technically speaking, any of our components could be nested if they have a selector defined in the Component decorator. But does it really make sense to nest a large view, such as our product list? For our purposes, we'll define a component as nestable if its template only manages a fragment of a larger view, if it has a selector so it can be used as a directive, and, optionally, if it communicates with its container.

We'll build a nested component. Then, we'll review how to use that nested component as a directive in a container component. We'll examine how to pass data to the nested component using a property with the Input decorator and how to pass data out of the nested component by raising an event defined with the Output decorator.

In our sample application, to improve the user experience, we want to replace the rating number displayed in the ProductListComponent with stars. We'll build the StarComponent and nest it within the ProductListComponent. We then refer to the outer component as the container or parent component, and we refer to the inner component as the nested or child component.

In our sample application, we want to change the display of the rating. Displaying the rating number using a visual representation, such as stars, makes it quicker and easier for the user to interpret the meaning of the number. This is the nested component we'll build.

Let's jump right in and build our StarComponent. When we last saw our sample application, we had completed the ProductListComponent. Now, of course, we want to change it. Instead of displaying a number for the rating here, we want to display stars.

```html
</td>
<td>{{product.productName}}</td>
<td>{{ product.productCode | lowercase | convertToSpaces:'-' }}</td>
<td>{{ product.releaseDate }}</td>
<td>{{ product.price | currency:'USD':'symbol':'1.2-2'}}</td>
<td>{{ product.starRating }}</td>
</tr>
```

Instead of adding the code to the ProductListComponent to display the stars, we want to build it as a separate component. This keeps the template and logic for that feature encapsulated and makes it reusable.

So let's begin by creating a StarComponent. The StarComponent can be used by any feature of the application, so it really doesn't belong in our products folder. We'll instead put it in a shared folder, where we'll put all our shared components.

Let's take a quick look at the style sheet. Notice that we have a style here that helps with cropping our stars.

Now we are ready to build the StarComponent. We begin by creating a new file. We'll name it star.component.ts.

```typescript
import { Component } from "@angular/core";

@Component({
  selector: 'pm-star',
  templateUrl: "./star.component.html",
  styleUrls: ['./star.component.css']
})
export class StarComponent {

}
```

We then create this component just like we'd create any other component, starting with the class, export class StarComponent. Next we decorate the class with the Component decorator. Recall that it is this Component decorator that makes this class a component. As always, it shows us a syntax error here because we are missing our import.

Time to set the Component decorator properties. For the selector, we'll set `pm-star`. For the templateUrl, we provide the path to the HTML file provided with the starter files. We'll add the styleUrls property, and in the array, we'll set the first element to the path of the style sheet that was also provided. Since both files are in the same folder as the component, we can use relative pathing.

Let's take a peek at the StarComponent template.

```html
<div class="crop"
  [style.width.px]="cropWidth"
  [title]="rating">
  <div style="width: 75px">
    <span class="fa fa-star"></span>
    <span class="fa fa-star"></span>
    <span class="fa fa-star"></span>
    <span class="fa fa-star"></span>
    <span class="fa fa-star"></span>
  </div>
</div>
```

Here it displays five stars using the Font Awesome star icon from the style sheets we imported earlier in this book. The div element sets the size for displaying the 5 stars to 75 px. The outer div element then crops the 75 px based on a defined cropWidth. This technique can then display partial stars, such as 4.5 of the 5 stars, by setting the cropWidth such that only 4.5 of the stars appear.

Recall what this syntax is called? This is property binding. We are using it here to bind the title property to display the numeric rating value. For these bindings to work, we need two properties in the component class, the rating number and the cropWidth.

Going back to the StarComponent, we'll add the two properties.

We want a rating property, which is a number and defines the actual rating value. Since we don't yet have a way to get this value from the container, let's hard code it to 4 for now so we'll see some stars.

And we need the cropWidth. We'll default it to 75, which is the width of our 5 stars as defined in the template. This value is then recalculated based on the rating.

Where do we put that calculation? Well we'd want the cropWidth recalculated anytime the container changes the rating number. So let's tap in to the OnChanges lifecycle hook as we discussed in the last module. We'll implement the OnChanges interface, import OnChanges, and write code for the ngOnChanges method identified in the OnChanges interface.

In this method, we'll assign the cropWidth using the rating. The total size of the 5 stars is 75 px. So each star is approximately 75 divided by 5 px. We multiply that by the rating number to get the cropWidth. For example, if the rating is 4, 4 times 75 divided by 5 is 60 pixels. So we'd crop the display of stars to 60 px, effectively only showing 4 of the stars.

```typescript
import { Component, OnChanges } from "@angular/core";

@Component({
  selector: 'pm-star',
  templateUrl: './star.component.html',
  styleUrls: ['./star.component.css']
})
export class StarComponent implements OnChanges {
  rating: number = 4;
  cropWidth: number = 75;

  ngOnChanges(): void {
    this.cropWidth = this.rating * 75/5;
  }
}
```

Our component is complete, and we are ready to nest it in another component. We are ready to nest our new component within another component.

```typescript
@Component({
  selector: 'pm-products',
  templateUrl: './product-list.component.html'
})
export class ProductListComponent { }
```

Here is a shortened form of the code for a container component and its template, and here is the nested component we just created. Instead of displaying the starRating number, we want to display the stars, so we nest the StarComponent in the template using the star component's selector as a custom HTML tag.

```typescript
@Component({
  selector: 'pm-star',
  templateUrl: './star.component.html'
})
export class StarComponent {
  rating: number;
  cropWidth: number;
}
```

This identifies where in the container to place the nested component's template. With the custom HTML tag in place, we are now using the nested component as a directive.

When we use the component as a directive, we need to tell Angular how to find that directive. We do that by declaring the nested component in an Angular module. How do we know which Angular module? Well, we still only have one Angular module, AppModule. In our example, the ProductList component's template wants to use the StarComponent, so we add the declaration to the same Angular module that declares the ProductList component.

```typescript
...
import { StarComponent } from './shared/star.component';

@NgModule({
  imports: [
    BrowserModule,
    FormsModule
  ],
  declarations: [
    AppComponent,
    ProductListComponent,
    ConvertToSpacesPipe,
    StarComponent
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

We define the nested component in the declarations array of the @NgModule decorator and, as always, define what we need by adding an import statement. Our star.component is now shown here on the right. We want to use our star.component in the ProductList template that is here on the left.

![](img/0155736aec718cf18821e9f10a5d308d_153_0.png)
