```
7  export class ProductListComponent {
8  |  pageTitle: string = 'Product List';
9  |  imageWidth: number = 50;
10 |  imageMargin: number = 2;
11 |  showImage: boolean = false;
12 |  products: any[] = [
13 |  {
```

And let's set its default value to false, so the images are not displayed when the page is first loaded. Next, we build the method that the event binding will call. By convention, methods are normally created after all of the properties are defined. So we'll put it down here. Let's name the method toggleImage. Notice that TypeScript does not require any keyword, such as function. Following the method name with open and closing parentheses identifies it as a method. Our method won't have a return type, so we specify the return type as void. The body of the method simply toggles the state of the showImage property. The bang or exclamation point used here is the logical not operator. It returns false if its operand, showImage in this case, is true and true if showImage is false, basically toggling the value from true to false or false to true.

```
toggleImage(): void {
|  this.showImage = !this.showImage;
}
```

Back in the template, we are ready to set up the event binding. On the button element, we define the click as the target event by enclosing it in parentheses. We assign it to our method enclosed in quotes. When the user clicks the button, the binding calls our method.

```
<th>
  <button class='btn btn-primary'
    (click)='toggleImage()'>
    Show Image
  </button>
```