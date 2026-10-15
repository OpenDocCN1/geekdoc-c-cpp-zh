```
@Component({
  selector: 'pm-products',
  templateURL: './product-list.component.html'
})
export class ProductListComponent {
  onNotify(message: string): void { }
}
```

What is our goal? When the user clicks on one of the star ratings, we want to display that rating in the product list component header. This feature may not be incredibly useful, but it demonstrates how to pass events from our nested child component to the parent container component. We added event binding to the nested component. When the user clicks on the stars, it logs a message. We instead want to send an event to the container component with that string message. We are back in the sample application, looking at the star.component, component, and template.

![](bbox=[0.12, 0.57, 0.91, 0.85])

Recall how the nested component sends data out to its container, it uses an event with the Output decorator. Let's define a ratingClicked