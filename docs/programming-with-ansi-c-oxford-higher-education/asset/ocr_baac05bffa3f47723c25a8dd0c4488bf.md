```
cout << "The size of StudMarks is " << StudMarks.size() << endl;
list<Student>::iterator index;
for(index = StudMarks.begin(); index != StudMarks.end(); ++index)
cout << *index << endl;
}
```

# Output

Enter mark for roll number 1 Enter -1 to stop: 13
Enter mark for roll number 2 Enter -1 to stop: 23
Enter mark for roll number 3 Enter -1 to stop: 34
Enter mark for roll number 4 Enter -1 to stop: 45
Enter mark for roll number 5 Enter -1 to stop: 32
Enter mark for roll number 6 Enter -1 to stop: 23
Enter mark for roll number 7 Enter -1 to stop: 24
Enter mark for roll number 8 Enter -1 to stop: 1
Enter mark for roll number 9 Enter -1 to stop: -1
The size of StudMarks is 8
The mark of roll number 1 is 13
The mark of roll number 2 is 23
The mark of roll number 3 is 34
The mark of roll number 4 is 45
The mark of roll number 5 is 32
The mark of roll number 6 is 23
The mark of roll number 7 is 24
The mark of roll number 8 is 1

# How the Program Works

The program does the same job as Program 16.4 with only one change in it; 'vector' is replaced by 'list' everywhere. The output of the program using the vector has not been given. It is the same as the output given for this program. This shows how easy it is to learn more containers once we learn one.

# List vs Vector

Lists seem to work similar to vectors. Why are they provided then? The emphasis is on three operations, namely, insertion, deletion, and access. The list is implemented using a doubly linked list; hence, insertion and deletion at random require reshuffling the pointers alone, and it is very fast. Unfortunately, accessing a random member requires moving to that place from either the beginning or the end, which is not efficient. A list is better when insertion and deletion at random places are to be performed, and access to elements is not done in random but in sequence. This is similar to the advantage of linked list over arrays.

> Note
> Vectors can grow automatically, but it comes with a cost. Extending a vector is similar to having a new large vector and copying the old vector elements in it. This is a linear time operation, that is, the time of insertion depends on the number of elements in the vector. On the other hand, growth in a list is a constant time operation, that is, the time of insertion remains constant irrespective of the number of elements to be inserted.

Table 16.2 lists the differences between a vector and a list.

There is a difference between Programs 16.4 and 16.2. The for loop does not contain test such as index < StudMarks.end() because operator '<' is not overloaded for bidirectional iterators provided by the list. It is only available for random access iterators. Fortunately, there is the inequality operator '!=' overloaded for bidirectional operators. Thus, the '!='