From the interface above, we see that given a string argument, the repository allocates the corresponding command. The interface employs a smart pointer return type to make explicit that the caller owns the memory for the newly constructed command.

Let’s now consider what an implementation for allocateCommand() might look like. This exercise will assist us in modifying the design for more flexibility.

```
unique_ptr<Command>
CommandRepository::allocateCommand(const string& c) const
{

if(c == "+") return make_unique<Add>();
else if(c == "-") return
make_unique<Subtract>(); // ... all known
commands ...
else return nullptr;

}
```

The above interface is simple and effective,