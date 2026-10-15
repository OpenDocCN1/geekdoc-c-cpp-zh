
This is a depiction of the DOM, or Document Object Model. The Document Object Model is a document model loaded into the browser and represents our HTML as a node tree where each node is a part of our HTML. Notice these scripts listed here. These aren't in our source index.html file. We'll talk about these bundles, what they are, and how they got here in the Building, Testing, and Deploying with the CLI chapter later in this book. Here is our selector tag. Open the selector tag and we see the HTML that we defined in our component's template.

![](img/0155736aec718cf18821e9f10a5d308d_62_0.png)

This view is a great way to see the HTML for the rendered page. There is also a debugger option available here on the Sources tab to view and debug our code.

![](img/0155736aec718cf18821e9f10a5d308d_63_0.png)

Since the Angular CLI uses webpack, our TypeScript files are listed under the webpack node here. And because the Angular CLI serve feature generates the map files, we can debug our TypeScript code directly.

![](img/0155736aec718cf18821e9f10a5d308d_63_1.png)

We can set a breakpoint, refresh the browser, and it hits that breakpoint.

![](img/0155736aec718cf18821e9f10a5d308d_64_0.png)

Use these debugging features anytime you need them. Before we move on, let's talk about what to do if something goes wrong. Because browsers don't understand the components and templates we build, Angular applications require a compile process to convert our templates and TypeScript code into JavaScript. If that compiler finds any HTML elements or code it doesn't understand, it displays a syntax error. In this example, I misspelled string. In both Angular and TypeScript, casing matters. That means that a property variable declared pagetitle with a lower case p is not the same as a property declared pageTitle with an uppercase P.

![](img/0155736aec718cf18821e9f10a5d308d_64_1.png)

```
export class AppComponent {
  pageTitle = 'Acme PM';
  PageTitle = 'Something else';
}
```

The same is true for all the keywords, class and function names, decorators, directives, and so on. Components must be declared in an Angular module. You can think of an Angular module as a project file that references all the component parts of the application. If something went wrong when adding a component, recheck your modules and ensure the component is referenced. Your code editor is often the best place to start if your application isn't working. VS Code will add a squiggly line under any syntax it doesn't understand. Hover over the line to view details on the error. Clicking on the underlined text will display a quick fix icon if there is one available. Open the VS Code terminal to view any displayed compiler messages.

![](img/0155736aec718cf18821e9f10a5d308d_65_0.png)

![](img/0155736aec718cf18821e9f10a5d308d_65_1.png)

If there are multiple messages in the terminal, scroll up to the first message after the last compile. Often, the first error is the root of the problem, causing the other errors. And if you see an error and don't know how to fix it, check out the list of common errors and their solutions in the Angular documentation. Sometimes it helps to stop and restart the compiler. Use Ctrl+C to stop and npm start to restart. The browser's developer tools can also be helpful. The console will display errors, messages, and debug information. Again, scroll up to the first message after the last compile as that error is often the root of the problem.

![](img/0155736aec718cf18821e9f10a5d308d_66_0.png)

If you see Cannot GET in the browser, that often means an error prevented the compiler from completing. And it didn't create the JavaScript files that the browser needs, so the browser couldn't get them. If this occurs, use the VS Code terminal window to view the errors. If you see an error or the application just doesn't work, it's helpful to recheck the recent code you've written. For any HTML, be sure the tags are correctly closed and that all the Angular directives are correctly spelled and cased. For the TypeScript code, be sure the braces are all properly closed. Just like JavaScript, TypeScript is case-sensitive so ensure everything has the appropriate case. Following these suggestions should get you back on the path to success with Angular. Now let's finish up with some checklists we can use as we build our own components. Angular is all about components, so our first set of checklists are for building a component. We create a class for the component with code to support the view, we use a decorator to define the component metadata, which includes the HTML for the component's template, and we import what we need. When creating the component class,

we give it a clear name. This is not only the name of the class, but the name of the component as well. Be sure to watch the casing since JavaScript is case-sensitive. By convention, use PascalCasing, whereby every word of the name is capitalized. It is common to append Component to the end of the class name to make it clear that it is a component class. Be sure to include the export keyword on the class signature. Recall what the export keyword does? It makes the class accessible to be imported by other parts of the application. If the component view displays data, such as a title, the data element is defined as a property of the class. To leverage TypeScript's strong typing, be sure to set the appropriate data type for each property and set a default value where appropriate. Use camelCase for property names with the first letter lowercase. If the component view has functionality, such as hiding and showing an image, the logic is defined as methods in the class. Use camelCase for method names with the first letter lowercase. How do we define the metadata for our component? If you said a Component decorator, you are right. A class is not a component unless it has a Component decorator. Be sure to prefix the decorator with an @. Since a decorator is a function, add parentheses and pass in the appropriate object properties. Use the selector property to define the name of the component when used as a directive in HTML. Be sure to prefix the selector for clarity.

```typescript
@Component({
  selector: 'pm-root',
  template: `
    <div><h1>{{pageTitle}}</h1></div>
  `
})
```

Note that the selector property is not needed if the component is not used in any HTML. Use the template property in the component metadata to define the view's HTML. Since we define the HTML in a string literal, we often get no IntelliSense or syntax checking. So take care to define correct HTML syntax. We'll see alternate ways to create the template for a component in the next chapter. But why do we need to use import? The import statement tells Angular where to find the members that this component needs. The import statement requires the import keyword followed by the member name and path. Take care when defining the member name as it is case-sensitive. The path to the file must be enclosed in quotes and is also case-sensitive. And remember that we don't need to specify the file extension. In summary, we rebuilt the AppComponent and have the very basics of our application working. Next, let's take a closer look at templates and how Angular can power them up with binding and directives as we start building the ProductList component.

## Chapter 7 How to Build Template & Component

To build a user interface for our application in Angular, we create a template with HTML. To power up that user interface, we need Angular's data binding and directives. In the next few chapters, we create the user interface using templates, directives, and data binding. Web applications are all about the user interface, and Angular makes it easier to build rich and powerful user interfaces. Angular gives us data binding so we can easily display information and respond to user actions. With Angular directives, we add logic to our HTML, such as if statements and for loops. With Angular components, we build nested user interface fragments, such as an image rotator or rating stars. We've seen that an Angular component is a view defined with the template, its associated code, defined with a class, and additional information, defined with metadata, and set using a component decorator. We'll focus on techniques for building the template. We evaluate the different ways we can build a template for our component and demonstrate how to create a linked template for our view. Then we'll build a component associated with that template and use it as a directive. We'll detail how to set up data binding using interpolation and display the value of our component class properties in the view. We need some basic logic in the template, so we'll leverage Angular's directives. We'll also look at additional data binding techniques. Looking at our application architecture, we currently have the index.html file and our root app component in place. So we have a working sample application, but it doesn't look like much. What we really want is a list of products. We'll begin
