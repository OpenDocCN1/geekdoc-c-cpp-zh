```
T = A(I)
A(I) = A(J)
A(J) = T
end
end if
end
4. stop
```

# 1.6.3 Purpose

The purpose is a brief description about what the algorithm does. It should be as brief as possible, describing the general algorithm processing, but should not describe all of the processing. For example, in Algorithm 1.1, the purpose just tells that this algorithm sorts the array of integers and does not need to state that the array is sorted and where the result is stored. Algorithm 1.2 searches for an element in an array.

# ALGORITHM 1.2

```
Algorithm search (val list<array>, val X<integer>)
Pre list containing data array to be searched and
argument containing data to be located
Post None
Return Location
1. Let list be the array and X be the element to be searched
2. For I = 1 to N do begin
if(List(I) = X)
then
Return I
end if
end
end
3. Return -1
4. stop
```

# 1.6.4 Condition and Return Statements

The pre condition states the pre-requisites for the parameters, if any. For example, in an algorithm for set operations, the pre condition may state that the input should be a group of elements without duplicates. Sometimes, there are no pre conditions, in which case, we still list the pre condition with the statement Nothing, as shown here.

Pre Nothing

If there are several input parameters, then the pre condition should be shown for each.
For example, a simple array search Algorithm 1.2 has the following header:

```
algorithm search (val list<array>, val argument<integer>)
```