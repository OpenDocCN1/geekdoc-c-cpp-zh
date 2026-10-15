implements keyword and the interface name to the class signature. Then be sure to write code for every property and method declared in the interface to fully implement the feature. We can encapsulate the styles for our component in the component itself.

```
@Component({
  selector: 'pm-products',
  templateUrl: './product-list.component.html',
  styleUrls: ['./product-list.component.css']
})
```

That way, the styles required for the component are associated with the component alone and don't leak into any other parts of the application. Use the styles property of the @Component decorator to specify the template styles as an array of strings. Use the styleUrls property of the component decorator to identify an array of external stylesheet paths. The specified styles are then encapsulated in the component. Lifecycle hooks allow us to tap into a component's lifecycle to perform operations.

```
import { Component, OnInit } from '@angular/core';

export class ProductComponent implements OnInit {
  ngOnInit(): void {
    console.log('In OnInit');
  }
}
```

The steps for using a lifecycle hook are: Import the lifecycle hook interface, implement the lifecycle hook interface in the Component