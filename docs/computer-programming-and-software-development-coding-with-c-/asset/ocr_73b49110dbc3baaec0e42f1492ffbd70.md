# Chapter 4 How to Define the Metadata with a Decorator

A class becomes an Angular component when we give it component metadata. Angular needs that metadata to understand how to instantiate the component, construct the view, and interact with the component. We define a component's metadata with the Angular component function.

```
```typescript
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

In TypeScript, we attach that function to the class as a decorator. A decorator is a function that adds metadata to a class, its members, or its method arguments. A decorator is a JavaScript language feature that is implemented in TypeScript. The scope of the decorator is limited to the feature that it decorates. A decorator is always prefixed with an @ sign. Angular has several decorators we use to provide additional information to Angular. We apply a decorator by positioning it immediately in front of the feature we are decorating.