
```cpp
while(true){
    cout << "Roll number: ";
    int rollNo;
    cin >> rollNo;

    if(rollNo == -1) break;

    if(rollNo < 1 || rollNo > 100)
        cout << "Invalid roll number." << endl;
    else
        cout << "Marks: " << marks[rollNo-1] << endl;
}
```

## 13.2.3 Who got the highest?

Having read in the marks as above, suppose we wish to print out the roll numbers of the student(s) who got the highest marks, instead of answering student marks queries.

What we want can be done in 2 steps. In the first step we determine the maximum marks obtained. In the second, we print out the roll numbers of all who got the maximum marks.

In Section 3.4.1 we have already discussed how to find the maximum of the numbers read from the keyboard. Now instead of getting the marks from the keyboard, we are required to read them from the array. Basically, instead of reading from the keyboard, the first element will be obtained from marks[0], and subsequent elements by looking at marks[i], where i has to go from 1 to 100. The code for this is as follows.

```cpp
float maxSoFar = marks[0];
for(int i=1; i<100; i++)    // i starts at 1 because we already took marks[0]
    if(maxSoFar < marks[i])
        maxSoFar = marks[i];
}
```

The next step is to print the roll numbers of those students who got marks equal to maxSoFar. This is easily done, we examine each marks[i], for all i as i goes from 0 to 99, and whenever we find marks[i] equalling maxSoFar, we print out i+1, because we stored the marks of roll number i+1 at index i.

```cpp
for(int i=0; i<100; i++)
    if (marks[i] == maxSoFar)
        cout << "Roll number " << i << " got maximum marks." << endl;
```

## 13.2.4 General roll numbers

In the code above, we exploited the fact that the roll numbers are consecutive. In general this may not happen. Often, the roll number assigned to each student may encode different kinds of information, e.g. first two digits are year of joining, another digit indicates the department to which the student belongs, and so on. Sometimes the roll number may also contain letters, though for simplicity we will ignore this possibility.

We consider the marks display problem in this new setting. We will use an additional array rollno in which to store the roll number, in addition to the array marks used above. The teacher first types in 100 pairs of number, each pair consisting of a roll number and the marks obtained by the student having that roll number. Our program must read in the roll number and marks and store them in the arrays rollno and marks. In the second phase, when a student types in a roll number, we must first look for it in the array rollno. If it is found, then we print the corresponding marks.

```
int rollno[100];
double marks[100];

for(int i=0; i<100; i++) cin >> rollno[i] >> marks[i];

while(true){
    int r; cin >> r; // roll number whose marks are requested
    if(r == -1) break;
    for(int i=0; i<100; i++)
        if(rollno[i] == r) cout << marks[i] << endl;
}
```

This idea, scanning an array from the beginning to the end in order to determine if a certain element is stored in the array, is sometimes called linear search.

The code above is unsatisfactory in two ways. First, if the given value r is not present in the array, it would be polite to print a message to that effect. Second, once we find r at some index, there is no need to scan the remaining elements. Both these goals can be achieved by replacing the for loop above with the following.

```
int i;
for(i = 0; i<100; i++){
    if(rollno[i] == r){ cout << marks[i] << endl; break;}
}
if(i >= 100) cout << "Invalid roll number.\n";
```

Note first that we break out of the loop upon finding a match. Thus, if a match is found the variable i (which has now been defined outside the loop) will have a value less than 100. The check at the end succeeds only if all 100 iterations were executed without finding a match, i.e. if the roll number r is invalid.

## 13.2.5 Histogram

Our next example is trickier, and it illustrates an important powerful feature of arrays.

Again, we have as input the marks of students in a class. Assume for simplicity that the marks are in the range 0 through 99. We are required to report how many students got marks between 0 and 9, how many between 10 and 19, how many between 20 and 29 and so on. As you might know, what we are asked to report is often called a histogram in Statistics².

We are required to report 10 numbers. So it could seem natural to use an array of 10 elements. The 0th element of the array can be used to count the number of marks in the range 0-9, the first element for the range 10-19 and so on. So in general we could say i th element of the array should correspond to the range i*10 to (i+1)*10-1 (both inclusive). So we call the array count and define it as:

```
int count[10]; // count[i] will store the number of marks in the range
// i*10 through (i+1)*10 -1.
```

Clearly, we should set the counts to 0 at the beginning, and change them as we read in the marks.

```
for(int i=0; i<10; i++)
    count[i]=0;
```

When we read the next mark, how do we decide which count to increment? It is natural to write something like the following.

```
for(int i=0; i< 100; i++){
    float marks;
    cin >> marks;
    if(marks <= 9) count[0]++;
    else if(marks <= 19) count[1]++;
    else if(marks <= 29) count[2]++;
    else if(marks <= 39) count[3]++;
    else if(marks <= 49) count[4]++;
    else if(marks <= 59) count[5]++;
    else if(marks <= 69) count[6]++;
    else if(marks <= 79) count[7]++;
    else if(marks <= 89) count[8]++;
    else if(marks <= 99) count[9]++;
    else cout << "Marks are out of range." << endl;
}
```

This works, but there is a better way! Suppose we read a mark m, which count should we increase? For this we simply need to know the tens place digit of m. As you might observe, this is simply ⌊m/10⌋, i.e. the integer part of m/10. But we can get the integer part by storing into an integer variable! This is what the following code does.

```
for(int i=0; i< 100; i++){
    float marks;
    cin >> marks;
    int index = marks/10;
```

²In general a histogram is a count of number of observations (marks, in our case) falling in various ranges of values (in our case the intervals 0-9, 10-19 and so on). The counts are often depicted as a bar chart, in which the height of the bars is proportional to the count and width to the size of the range.

```
if(index >= 0 && index <= 9) count[index]++;
else cout << "Marks are out of range." << endl;
}
```

Note that this works only because all the ranges are of the same size. But this is very often the case when computing histograms.

## 13.2.6 A taxi dispatch program

Suppose you are the Mumbai dispatcher for the Mumbai-Pune taxi service. Your job is as follows. Drivers of taxis that are willing to take passengers to Pune report to you and give you their driver ID number and wait. Passengers who want taxis also report to you. When a passenger reports, you check if there are any waiting taxis. If there are, you assign the taxi of the driver that reported to you the earliest. Clearly, once a taxi has been given to a passenger, you need not keep the corresponding ID number on your list. If no taxis are available, you let the passenger know. You are not expected to keep track of waiting passengers, though an exercise asks you to do precisely this. You may assume that at any given point there will not be more than 100 taxis waiting for passengers. You are to write a program which will help you dispatch taxis as required.

Let us make this more specific. Suppose that the dispatcher will type 'd' when a driver arrives, followed by the driverID. Likewise when a customer arrives, the dispatcher will type 'c', and expect the program to print the ID of the assigned driver. Finally, to terminate the program, we will have the dispatcher type 'x' (commonly used as abbreviation of eXit).

Next we decide what variables we might need and how we should be using them.

Clearly, we will need to store the IDs of the waiting drivers. It seems natural to use an array, say driverID, to store these. Assume for simplicity that the IDs are integers with 9 or fewer digits, i.e. that they will fit in int. The size of the array can be a number larger than the number of drivers we expect will be waiting with us at any time. Most of the time there will be fewer drivers waiting with us than the size of the array, so we presumably need a variable nWaiting which will denote the number of waiting drivers.

We also need to somehow record the order in which the drivers arrived, because we want to assign the next customer to the driver who has registered with us the earliest. A natural way to do this is to store the earliest waiting driver at index 0, the next earliest at index 1, and so on. The ID of the driver that arrived last would be at index nWaiting - 1.

If a new driver arrives, we can store his ID at the index nWaiting, and increment nWaiting. If a customer arrives, we can assign the driver at driverID[0]. However, once we assign the driver, we must shift up all the other entries in the array, since we have decided that the waiting drivers must be stored starting at index 0. This is expressed in the following code.

```
const int n = 100; // estimate of max waiting drivers.
int driverID[n], nWaiting = 0;

while(true){ /* Invariants: nWaiting denotes the number of waiting drivers.
    0 <= nWaiting <= n. IDs of waiting drivers are in driverID,
    from driverID[0] to driverID[nWaiting - 1] */
```
