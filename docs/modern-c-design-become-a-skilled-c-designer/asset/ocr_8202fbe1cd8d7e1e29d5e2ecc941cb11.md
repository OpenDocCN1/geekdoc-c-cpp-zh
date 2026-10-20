precondition is trivial; we ensure at least one element is on the stack. If not, an exception is thrown:

```
void
UnaryCommand::checkPreconditionsImpl()
const
{
if(Stack::Instance().size() < 1)
throw Exception{"Stack must have one
element"}; }
```

The executeImpl() command is also quite straightforward:

```
void UnaryCommand::executeImpl() {
top_ = Stack::Instance().pop(true);
Stack::Instance().push( unaryOperation(top_)
);
}
```

The top element is popped from the stack and stored in the UnaryCommand’s state for the purposes of undo. Remember, because we have already checked the precondition, we can be assured that unaryOperation() will complete without an error. Commands with