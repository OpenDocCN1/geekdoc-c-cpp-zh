This type of search is known as the sequential search because each element of the array may potentially be referenced in order to find the desired element or to determine that element does not exist. What is the goodness of the sequential searching algorithm?
• It works! It is simple.
What problems are associated with the use of the sequential searching algorithm?

What if we had a very large data set and the value we are looking for does not exist?
• It would take a long time to search every element and make this determination.
What if multiple instances of the target value are potentially present in the array?
• The entire array must now be searched to find every instance of a target in an unsorted array.

# The Binary Search

It is possible to reduce the time (both average and worst-case) it takes to complete a search by using an alternative searching algorithm known as the binary search. The binary search does require that the data in the array be sorted.

Is there a cost associated with sorting data?
• Yes, but if we search our data frequently it is worth paying the cost of sorting and maintaining our data in a sorted state.

Should the binary search always be used when searching?
• No, only when the data set is large and searched frequently.

# New Integer Variables in the Binary Search

+   • first – This integer will represent the lowest index value at which the target value may potentially be found in the array.

+   • last – This integer will represent the highest index value at which the target value may potentially be found in the array.

+   • mid – The average of the first and last variables will determine where in the array the next comparison will be made with the target value. The mid is updated at the start of every iteration of the binary search process.

How and when are the first and last variables updated? When the value at the mid is less than the target then the first is set to the value of the mid plus one. When the value at the mid is greater than the target then the last is set to the value of the mid minus one.