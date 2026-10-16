# Working with Blocks

One of the newest and most powerful additions to Objective-C is the inclusion of a capability known as blocks. Using them, you can specify arbitrary portions of code which can be passed around to methods and functions like objects. In this chapter, I show you how to use them.

# Understanding Blocks

If you are coming to Objective-C from another language, such as Ruby or lisp, you may already be familiar with the concept of blocks, also known as closures. Listing 5.1 shows an example of a block in Ruby.

Listing 5.1

# An example block in Ruby

```
items.each { |item| puts item }
```

Essentially, a block enables you to define a function object in-line in your code. These function objects can be referenced by using traditional variables, including being passed to other functions. What this means, is that you can define reusable chunks of code that function and can be passed around just like objects enabling that code to be executed inside other objects, dynamically. This may sound confusing, but I think as we work through the upcoming examples, the concept will become clearer.

In the case of the above block, this code is actually iterating over each item in the items array, and then executing the code inside the curly braces, passing the current item into the block.

# In This Chapter

+   - Using blocks to encapsulate algorithms
+   - Using the block directive
+   - Creating map and filter functions using blocks
+   - Running blocks in parallel using threads and Grand Central Dispatch