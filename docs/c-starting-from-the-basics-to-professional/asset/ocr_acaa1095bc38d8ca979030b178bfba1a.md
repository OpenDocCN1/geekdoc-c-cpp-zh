This snippet will compile and run. But now think about what the default assignment operator of the Message class does exactly during this last statement. It copies the m_text member from the source Message onto that of the Message object. This member is just a raw pointer variable, though, so after the assignment we have two different Message objects whose m_text pointer refers to the same memory location. Once both Messages go out of scope the destructors of both objects will therefore apply delete[] on the same location! It's impossible to tell what the result of this second delete[] will be. One likely outcome, though, is a program crash.

So, clearly, the default assignment operator will not do for classes that manage dynamically allocated memory themselves. You therefore have no other option but to redefine the assignment operator for Message. (Besides switching to std::string, obviously. But you can't. For some reason...)

An assignment operator should return a reference, so in the Message class, it would look like this:

```
```
Message& operator=(const Message& message);    // Assignment operator
```
```

The parameter should be a reference-to-const and the return type a reference-to-non-const. As the code for the assignment operator will just copy data from the members of the right operand to the members of the left operand, you may wonder why it has to return a reference—or indeed, why it needs to return anything. Consider how the assignment operator is applied in practice. With normal usage you can write this:

```
```
message1 = message2 = message3;
```
```

These are three objects of the same type, so this statement makes message1 and message2 copies of message3. Because the assignment operator is right associative, this is equivalent to the following:

```
```
message1 = (message2 = message3);
```
```

The result of executing the rightmost assignment is evidently the right operand for the leftmost assignment, so you definitely need to return something. In terms of operator=(), this statement is equivalent to the following:

```
```
message1.operator=(message2.operator=(message3));
```
```

You have seen this several times before. This is called method chaining. Whatever you return from operator=() can end up as the argument to another operator=() call. The parameter for operator=() is a reference to an object, so the operator function must return the left operand, which is the object that is pointed to by this. Further, to avoid unnecessary copying of the object that is returned, the return type must be a reference.

Here is a reasonable first attempt at a definition of an assignment operator for Message:

```
```
Message& operator=(const Message& message)
{
  delete[] m_text;                            // Delete the previous char array
  m_text = new char[std::strlen(message.m_text) + 1]; // Replace it with a new array
  std::strcpy(m_text, message.m_text);        // Copy the text (mind the order!)
  return *this;                               // Return the left operand
}
```
```

The this pointer contains the address of the left operand, so returning *this returns the object. This function looks okay, and it appears to work. And in nearly all cases, it really does work just fine. Nevertheless, there is one serious fly left in the ointment. Suppose someone writes this:

```
```
message1 = message1;
```
```