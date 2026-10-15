The Output decorator is a function, so we add parentheses. We, again, use the quick fix to add output to the import statement. In this example, we are decorating only one property of the nested component with the Output decorator. but we aren't limited to one. We can expose multiple output properties as needed.

```
1 import { Component, EventEmitter, Input, OnChanges, Output }
2
3 @Component({
4   selector: 'pm-star',
5   templateUrl: './star.component.html',
6   styleUrls: ['./star.component.css']
7 })
8 export class StarComponent implements OnChanges {
9   @Input() rating: number = 0;
10  cropWidth: number = 75;
11  @Output() ratingClicked: EventEmitter<string> =
12    new EventEmitter<string>();
13
14  ngOnChanges(): void {
15    this.cropWidth = this.rating * 75/5;
16  }
17
18  onClick(): void {
19    console.log(`The rating ${this.rating} was clicked!`);
20  }
21 }
22
```

In our star components onClick method, instead of logging this message, we want to emit our ratingClicked event and pass the message to the container component. We use the event property and call its emit method passing in the desired string.