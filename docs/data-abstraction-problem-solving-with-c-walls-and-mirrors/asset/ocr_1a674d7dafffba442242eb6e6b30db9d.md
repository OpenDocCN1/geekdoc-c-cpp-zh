# 378 CHAPTER 13 Queues and Priority Queues

# FIGURE 13-3 The results of inserting the characters a, b, c, b, d into both a queue and a stack

| String: | Queue: | Stack: |
| --- | --- | --- |
| abcd | a b c b d | d -> Top |
| | Front Back | b |
| | | c |
| | | b |
| | | a |

palindrome. You can see that the first character in the string is at the front of the queue and the last character in the string is at the top of the stack. Thus, characters removed from the queue will occur in the order which they appear in the string, and characters removed from the stack will occur in the opposite order.

Knowing this, you can compare the characters at the front of the queue and the top of the stack. If the characters are the same, you can remove them. You repeat this process until the stack and queue become empty, if the original string is a palindrome, or the two characters are not the, in which case the string is not a palindrome.

The following is a pseudocode version of a nonrecursive recognition algorithm for the language of palindromes:

```
// Tests whether a given string is a palindrome.
isPalindrome(someString: string): boolean
// Create an empty queue and an empty stack
aqueue = a new empty queue
astack = a new empty stack
// Add each character of the string to both the queue and the stack
length = length of someString
for (i = 1 through length)
{
    nextChar = i-th character of someString
    aqueue.enqueue(nextChar)
    astack.push(nextChar)
}
// Compare the queue characters with the stack characters
charactersAreEqual = true
while (aqueue is not empty and charactersAreEqual)
{
    queueFront = aqueue.peekFront()
    stackTop = astack.peek()
    if (queueFront equals stackTop)
{
        aqueue.dequeue()
        astack.pop()
}
elelse
    charactersAreEqual = false
}
return charactersAreEqual
```