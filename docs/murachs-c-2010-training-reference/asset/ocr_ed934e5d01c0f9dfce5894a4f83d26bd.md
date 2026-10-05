# More skills for working with arrays

Now that you know how to work with one-dimensional, rectangular, and jagged arrays, you're ready to learn some additional skills for working with arrays.

# How to use the Array class

Because an array is actually an instance of the Array class, you can use the properties and methods of this class to work with your arrays. Figure 8-9 presents the properties and methods you are most likely to use.

You've already seen how to use the Length property and the GetLength method. Another property you may want to use is the GetUpperBound method, which returns the index of the last element in a given dimension of an array. The first example in this figure illustrates the difference between the GetLength and GetUpperBound methods. Here, you can see that the GetLength method returns a value of 4 for a one-dimensional array that contains four elements. In contrast, the GetUpperBound returns a value of 3 because the four elements are referred to with index values of 0 through 3.

Although values have been assigned to the elements of the array in this example, you should realize that the GetLength and GetUpperBound methods return the same values or not values have been assigned to the array. In other words, these methods depend only on the number of elements that were declared for the array. That's true of the Length property as well.

The Sort method of the Array class sorts the elements in a one-dimensional array. This is illustrated by the second example in this figure. Here, the first statement declares an array that consists of three names. Then, notice that because this is a static method it's called from the Array class, not from the array itself. After the array is sorted, a string is created that contains the values of the elements in ascending order. Then, the string is displayed in a message box.

The third example shows how you can use the BinarySearch method to locate a value in a one-dimensional array. This code uses the BinarySearch method to get the index of the specified employee in an employees array. Then, this index is used to get the corresponding sales amount from a salesAmounts array.

For the BinarySearch method to work properly, the array must be sorted in ascending sequence. If it's not, this method usually won't be able to find the specified value, even if it exists in the array. When the BinarySearch method can't find the specified value, it returns a value of -1. Then, if you try to use this value to access an element of an array, an IndexRangeException will be thrown.