Everything is jumbled together. It’s still better than searching through a long source code listing, but we can make it better using #pragma mark. Replace the following comment:

```
```objc
//Memory Management
```
```

with this:

```
```objc
#pragma mark -
#pragma mark Memory Management
```
```

Now the drop-down list of methods looks like this:

![](bbox=[0.24, 0.274, 0.67, 0.508])

The #pragma mark - draws the horizontal line separator, and #pragma mark Memory Management produces the bold heading.⁹ Introduce these headings in place of all of the sections, and your code becomes a lot more navigable, as we can see on the next page.¹⁰

Our desktop and iPhone web browsers have served us well. I’ve used them to illustrate creating classes in code and instantiating objects in code or in a nib. You’ve written and called methods with and without parameters.

9. Don’t add trailing spaces after the - or #pragma mark - will render as a dash instead of a horizontal line in the drop-down list.
10. If you synthesized each property on a separate line, they will appear on separate lines and not all on one line as mine do.