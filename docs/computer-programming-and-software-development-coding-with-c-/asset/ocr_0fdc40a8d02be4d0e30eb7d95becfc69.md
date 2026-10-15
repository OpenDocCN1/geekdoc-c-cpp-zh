```
import { Component } from '@angular/core';
```

We start with the import keyword. We identify the name of the member we need within curly braces. In this case, we need the Component decorator function. And we define the path to the library or file containing that member, in this case the angular/core library. If we need multiple members from the same library or file, we list them all in the imports list, separated by commas.

```
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

This is a component. Let's now build the first component for our sample application.