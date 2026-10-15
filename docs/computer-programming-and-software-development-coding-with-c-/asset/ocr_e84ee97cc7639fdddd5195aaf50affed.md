# Chapter 16 How to Build Custom Pipes

As we saw before, we use pipes for transforming bound properties before displaying them in a view. There are pipes that transform a single value or an iterable list of data. In this chapter, we want to build our own custom pipe. For our sample application, the product code is stored with a dash and displayed that way here, but the users would prefer to see the product code with a space instead. We could build a custom pipe to replace the dashes with spaces, but let's build a more generalized custom pipe that transforms any specified character in a string to a space. The code required to build a custom pipe may look somewhat familiar at this point.

```
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
    name: 'convertToSpaces'
})
export class ConvertToSpacesPipe implements PipeTransform {
    transform(value: string,
        character: string): string {
    }
}
```

It uses patterns similar to other code we've created in this book. Here is the class. We add a pipe decorator to the class to define it as a pipe. Similar to the other decorators we've used, this is a function, so we add parentheses. We pass an object to the function, specifying the name of the pipe. This is the name for the pipe used