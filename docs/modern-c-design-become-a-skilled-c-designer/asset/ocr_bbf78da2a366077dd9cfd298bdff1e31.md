command is quite simple:

```
void
CommandRepository::registerCommand(const string& name, unique_ptr<Command> c)
{

if( repository_. find(name) !=
repository_.end() ) // handle duplicate
command error
else
repository_.emplace( name, std::move(c) ); }
```

Here, we check whether or not the command is already in the repository. If it is, then we handle the error. If not, then we move the command argument into the repository, where the command becomes the prototype for the command name. Note that the use of unique_ptr indicates that registering a command transfers ownership of this prototype to the command repository. In practical usage, the core commands are all registered via a function in the CoreCommands.cpp file, and a similar function exists inside each plugin to register