
> **NOTE** You can download the code and resources for this lesson from the website at www.wrox.com/go/csharp24hourtrainer2e.

## Hints

- Try to figure out the Randomize method's declaration yourself before you read the step-by-step instructions that follow.

## Step-by-Step

- Start a new project and give it an ArrayMethods class.
  1. This is reasonably straightforward. You don't need to make the ArrayMethods class generic.

- Create a generic Randomize method with one generic type parameter T. The method should take as a parameter an array of T and randomize the items it contains.
  1. The following code shows how you can implement this method:

```csharp
class ArrayMethods
{
    // Make a Random object to use to pick random items.
    private static Random Rand = new Random();

    // Randomize the items in an array.
    public static void Randomize<T>(T[] items)
    {
        // For each spot in the array, pick
        // a random item to swap into that spot.
        for (int i = 0; i < items.Length - 1; i++)
        {
            // Pick a random item j between i and the last item.
            int j = Rand.Next(i, items.Length);

            // Swap item j into position i.
            T temp = items[i];
            items[i] = items[j];
            items[j] = temp;
        }
    }
}
```

- Make the main program test the method.
  1. The program I wrote uses two TextBoxes, one to hold the original items and one to display the randomized items. When you click the Randomize button, the following code executes:

```csharp
// Randomize the items and display the results.
private void randomizeButton_Click(object sender, EventArgs e)
{
    // Get the items as an array of strings.
    string[] items = itemsTextBox.Lines;

    // Randomize the array.
    ArrayMethods.Randomize<string>(items);

    // Display the result.
    randomizedTextBox.Lines = items;
}
```

Notice that the code uses the TextBox's Lines property to get the entered values. That property returns the lines in a multi-line TextBox as an array of strings.

Also notice that the code doesn't need to make an instance of the ArrayMethods class. That's the advantage of making the Randomize method static.

## EXERCISES

- 1. [Hard] The Randomize method in the Try It doesn't actually need to work with an array. What it really needs is to access items by index. The IList interface requires that a class provide a Count property and indexes.

  Write a new version of the generic Randomize method that takes as a parameter an IList. (Hint: You'll also need a type parameter for the items inside the list.) Update the program to test both versions of the method. Note that C# cannot infer which version to use if you don't include type parameters when the main program invokes the method.

- 2. Finish building the generic Alternate method described earlier in this lesson. Add the code needed to make the alternating version of the list. To make using the method easy, make it static in the ArrayMethods class. Make the main program test the method with lists containing odd and even numbers of items.

- 3. [Hard] The solution to Exercise 1 rearranges the items in an IList randomly. The same approach would be tricky for the Alternate method in Exercise 2 because it's not obvious how you would shuffle the items around in the same array without losing track of where they all belong. (At least I couldn't think of a good way to do it.)

  However, you can use a slightly different approach. Add an Alternate method to the ArrayMethods class that uses an intermediate array to arrange the items in an IList.

- 4. [Hard] Make the TreeNode class to represent a tree node associated with a piece of data of some generic type. In addition to the code shown earlier in this lesson, give the class:
  - An AddChild method that adds a new child node to the node for which the method is invoked. Have the method take a piece of data of the class's generic type as a parameter and return a new TreeNode representing that piece of data.
  - A private AddToListPreorder method that adds a node's subtree to a list in preorder format. The preorder format lists the node's data first and then recursively calls the method to add the data for the node's children. You can use code similar to the following:

```csharp
// Recursively add our subtree to an existing list in preorder.
private void AddToListPreorder(List<TreeNode<T>> list)
{
    // Add this node.
    list.Add(this);

    // Add the children.
    foreach (TreeNode<T> child in Children)
        child.AddToListPreorder(list);
}
```

  - A public Preorder method that returns the node's subtree items in a list in preorder format. The method should call AddToListPreorder to do all of the work. You can use code similar to the following:

```csharp
// Return a list containing our subtree in preorder.
public List<TreeNode<T>> Preorder()
{
    List<TreeNode<T>> list = new List<TreeNode<T>>();
    AddToListPreorder(list);
    return list;
}
```

  - For extra credit, add similar methods to build lists in postorder and inorder. In postorder, a node recursively adds its children to the list and then adds its own data. In inorder, a node recursively adds the first half of its children to the list, then itself, and then the rest of its children.

Make the main program build the tree shown in Figure 28-1, although it doesn't need to display it graphically as in the figure. Make the program display the tree's preorder, postorder, and inorder representations, as shown in Figure 28-2.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_443_0.png)

FIGURE 28-1

![](img/d5be6ade75773ca6cec5c78f96a98bb1_443_1.png)

FIGURE 28-2

- 5. Make a generic PriorityQueue class. The class is basically a list holding generic items where each item has an associated priority. Give the class a nested ItemData structure similar to the following to hold an item:

```csharp
// A structure to hold items.
private struct ItemData
{
    public int Priority { get; set; }
    public T Data { get; set; }
}
```

This structure is defined inside the PriorityQueue class and won't be used outside of the class, so it can be private. Note that this structure uses the class's generic type parameter T for the data it holds.

The class should store its ItemData objects in a generic List.

Give the PriorityQueue class a public Count property that returns the number of items in the list.

Give the class an AddItem method that takes as parameters a piece of data and a priority. It should make a new ItemData object to hold these values and add it to the list.

Finally, give the class a GetItem method that searches the list for the item with the smallest priority number (priority 1 means top priority), removes that item from the list, and returns the item and its priority via parameters passed for output. (If there's a tie for lowest priority number, return the first item you find with that priority.)

- 6. Make a generic Sack class that holds items with weights. Give the class the following features:
  - A constructor that takes as a parameter the Sack's total capacity.
  - An Add method that takes as parameters a data item and a weight. If the total weight in the Sack exceeds the Sack's capacity, the method should throw an ArgumentException.
  - An Items method that returns a List holding the items in the Sack.
  - A Weights method that returns a List holding the weights of the items in the Sack.

Build a user interface that lets the user add items with weights to a Sack with a capacity of 100. Use two ListBoxes to display the items in the Sack and their weights after each addition.

- 7. Make a program similar to the one you built for Exercise 6 except using a Box class. A Box should be similar to a Sack class except it should have a maximum total volume in addition to a maximum total weight.

- 8. Make a generic method that swaps its two parameters' values.

- 9. [Advanced] The Math.Min and Math.Max methods are very useful, but they have two big drawbacks. First, they take only two parameters. That means if you want to find the largest and smallest of more than two values, you need to use them repeatedly. (Other available methods, notably LINQ, are described in Lesson 36.)

The second drawback is that they only work with double parameters. If you pass ints or floats into the methods, the values are promoted to the double data type so the methods still work, but their results are doubles so you'll need to convert them if you want the results to have the original data types.

For this exercise, write generic Min and Max methods that can take any number of parameters and that return a value in the parameters' data type. Hints:
