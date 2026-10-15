Show Image. If we click it, it says Hide Image. That a little more user friendly. Before we move on, let's talk a moment about Angular's change detection. By default, Angular is constantly watching for changes to any bound properties and listening for events. In our sample application, we have a button that shows or hides images. In the HTML for the button, we bound its click event to a method in our component, and we used interpolation to change the text of the button based on the value of a property in our component.

```
<button class='btn btn-primary'
    (click)='toggleImage()'>
    {{showImage ? 'Hide' : 'Show'}} Image
</button>
```

```
export class ProductListComponent {
    pageTitle = 'Product List';
    showImage = false;

    toggleImage(): void {
        this.showImage = !this.showImage;
    }
}
```

We used the ngIf structural directive to add or remove the image element from the DOM.

```
<img *ngIf='showImage'
    [src]='product.imageUrl'
    [title]='product.productName'
```

The showImage property is initially false, so the button text displays Show Image, and the ngIf removed the image from the display.