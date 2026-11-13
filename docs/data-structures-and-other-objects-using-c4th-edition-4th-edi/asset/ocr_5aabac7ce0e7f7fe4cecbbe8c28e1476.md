# circular array

We do not need to move all the array elements. When the rear index reaches the end of the array, we can simply start reusing the available locations at the front of the array. Think of this arrangement as if the array were bent into a circle with the first component of the array immediately after the last component. In this way, the successor of the final array index is array index 0 []. In this circular arrangement, the free index positions are always “right after” data[last].

For example, suppose that we have a queue of characters with a capacity of five, and the queue currently contains three entries, ‘A’, ‘B’, and ‘C’. Perhaps these values are stored with first equal to 0 and last equal to 2, as shown here:

![](bbox=[0.38, 0.3, 0.7, 0.44])

The question marks indicate unused spots in the array.

Let’s remove two entries (the ‘A’ and ‘B’), and add two more entries to the rear of this queue, perhaps the characters ‘D’ and ‘E’. The result is shown here:

![](bbox=[0.38, 0.5, 0.7, 0.63])

At this point, first is 2, last is 4, and the queue elements range from data[2] to data[4]. Suppose that now we add another character, ‘F’, to the queue. The new entry cannot go after last, since we have hit the end of the array. Instead, we go to the front of the array, adding the new ‘F’ at location data[0], as shown here:

![](bbox=[0.38, 0.71, 0.7, 0.85])