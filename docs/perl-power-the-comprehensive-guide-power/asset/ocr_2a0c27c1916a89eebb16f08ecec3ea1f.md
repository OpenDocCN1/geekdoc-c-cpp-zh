the array, you then iterate through the array to verify that it has increased in size by one element. As Figure 7.12 shows, this is the case. The index value of the new element reveals the `push()` function has augmented the size of the array by one and assigned the new element to the position designated by the largest index value.

In the lines trailing comment #3, you repeat the actions of the code associated with comment #2. This time around, you add `Whyalla` to the array. Again, you iterate through the list using the scalar form of the array and display the index values of the list elements. In the data display Figure 7.12 provides, you can see that the new element possesses the highest index value.

![](bbox=[0.359, 0.3, 0.856, 0.511])

**Figure 7.12**  
As each element is pushed onto an array, it assumes the highest index value.

# Uses of Dynamic Arrays

The array Perl provides is known technically as a *dynamic* array. Dynamic arrays grow automatically. In other words, you can add items to them whenever you want, at any time during the execution of your program. In contrast, in other programming languages, you find *static* arrays, which are arrays that you set up once, with a fixed number of elements, and cannot change afterward. Perl does not provide such arrays. Its arrays are dynamic. You can add to them at any time.

The question then becomes *how* you want to add items to your arrays. How you add items to an array changes the array into a *container*. In simple terms, a container can be viewed as an array that you use in a special way, as when you add items to its beginning only or to its end only. The `push()`, `pop()`, `shift()`, and `unshift()` functions allow you to use arrays as containers. Among the containers are such entities as stacks, queues, lists, and vectors. Each of these containers is also known as a *data structure*. Data structures (containers) allow you to control the way that you add data to or remove data from an array.

Two frequently used data structures are called *stacks* and *queues*. You can apply the `push()` and `shift()` functions to the dynamic array Perl furnishes to transform it into a