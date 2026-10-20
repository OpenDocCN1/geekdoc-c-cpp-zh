
vptr in our objects, we cannot assume identical alignment. Therefore, plugin classes should not inherit from main application classes that have member variables defined in the base classes if these member variables are used in the main application. This follows since the main application’s compiler may use a different memory offset to a member variable than what was defined by the plugin’s compiler if each compiler uses different alignment. Fourth, due to name mangling variances across different compilers, exported interfaces must specify `extern "C"` linkage. The linkage requirement is bidirectional. Plugins should not call application functions without `extern "C"` linkage, nor should the application call plugin functions without `extern "C"` linkage. Note that because non-inline, non-virtual member functions require linkage across compilation units (as opposed to virtual functions, which are called via the vptr through an offset in the virtual function table), the application should only call into plugin code through virtual functions, and plugin code should not call base class non-inline, non-virtual functions compiled in the main application. Finally, exceptions are rarely portable across the binary interface between the main program and plugins, so we cannot throw exceptions in a plugin and try to catch them in the main application.

That was a mouthful. Let’s recap by enumerating the rules for C++ plugins: 1. Memory allocated in a plugin must be deallocated in the same plugin. 2. Standard library components cannot be used in plugin interfaces.

3. Assume incompatible alignment. Avoid plugins inheriting from main application classes with member variables if the variables are used in the main application.

4. Functions exported from a plugin (to be called by the main application) must specify extern "C" linkage. Functions exported from the main application (to be called by plugins) must specify extern "C" linkage.

5. The main application should communicate with plugin-derived classes exclusively via virtual functions. Plugin-derived classes should not call non-inline, non-virtual main application base class functions.

6. Do not let exceptions thrown in plugins propagate to the main application.

With these rules in mind, let’s return to the three fundamental problems we must solve in order to design plugins.

## **Problem 1: The Plugin Interface**

The plugin interface is responsible for several items. First, it must enable the discovery of both new commands and new GUI buttons. We’ll see that this functionality is most effectively accomplished through a class interface. Second, the plugin must support a C linkage interface for allocating and deallocating the aforementioned plugin class. Third, pdCalc should provide a PluginCommand class derived from

Command to assist in correctly writing plugin commands. Technically, a PluginCommand class is optional, but providing such an interface helps users conform to Plugin Rules 3 and 6. Fourth, it is worthwhile for the plugin interface to provide a function for querying the API version that a plugin supports. Finally, pdCalc must provide C linkage for any of the functions it must make available for plugins to call. Specifically, plugin commands must be able to access the stack. We’ll address these issues in sequence starting with the interface for discovering commands.

### The Interface for Discovering Commands

The first problem we face is how to allocate commands from plugins when we know neither what commands the plugin provides nor the names of the classes we’ll need to instantiate. We’ll solve this problem by creating an abstract interface to which all plugins must conform that exports both

commands and their names. First, let’s address what functionality we’ll need.

Recall from Chapter 4, that in order to load a new command into the calculator, we must register it with the CommandRepository. By design, the CommandRepository was specifically constructed to admit dynamic allocation of commands, precisely the functionality we need for plugin commands. For now, we’ll assume that the plugin management system has access to the register command (we’ll address this deficiency in Section 7.4). The CommandRepository’s registration function requires a string name for the command and a unique_ptr that serves as a prototype for the command. Since pdCalc knows nothing a priori about the command names in a plugin, the plugin interface must first make the names discoverable. Second, since C++ lacks reflection as a language feature, the plugin interface must provide a way to create a prototype command to be associated with each of the discovered names. Again, by design, the abstract Command interface supports the prototype pattern via

the clone() virtual member function. Let’s see how these two prior design decisions effectively enable plugins.

Based on the C++ plugin rules above, the only means we have to effect command discovery is to encapsulate it as a pure virtual interface to which all plugins must adhere. Ideally, our virtual function would return an associative container of unique_ptr<CommandPtr> values keyed by strings. However, our C++ plugin rules also stipulate that we cannot use standard containers, thus excluding string, map, unordered_map, and unique_ptr. Rather than (poorly) reimplementing custom versions of any of these containers, we’ll just use a typically avoided, low-level facility available to us: arrays of pointers.

The above design is enforced by creating a Plugin class to which all plugins must conform. The purpose of this abstract class is to standardize plugin command discovery. The class declaration is given by the following:

```
class Plugin
{
public:

Plugin();
virtual ~Plugin();

struct PluginDescriptor
{
int nCommands;
char** commandNames;
Command** commands;
};

virtual const PluginDescriptor&
getPluginDescriptor() const = 0; };
```

We now have an abstract plugin interface that, when specialized, requires a derived class to return a descriptor that provides the number of commands available, the names of these commands, and prototypes of the commands themselves. Obviously, the ordering of the command names must match the ordering of the command prototypes. Unfortunately, with raw pointers and raw

arrays, the ambiguity of who owns the memory for the command names and command prototypes arises. Our inability to use standard containers forces us into an unfortunate design: contract via comment. Since our rules dictate that memory allocated in a plugin must be freed by the same plugin, the best strategy is to decree that plugins are responsible for deallocation of the PluginDescriptor and its constituents. As stated before, the memory contract is “enforced” by comment.

Great, our problem is solved. We create a plugin, let’s call it MyPlugin, that inherits from Plugin. We’ll see how to allocate and deallocate the plugin in Section 7.3 below. Inside of MyPlugin, we create new commands by inheriting from Command as usual. Since the plugin knows its own command names, unlike the main program, the plugin can allocate its command prototypes with the new operator. Then, in order to register all the plugin’s commands, we simply allocate a plugin descriptor with both command names and command prototypes, return the

descriptor by overriding the getPluginDescriptor() function, and let pdCalc register the commands. Since Commands must each implement a clone() function, pdCalc can copy the plugin command prototypes via this virtual function to register them with the CommandRepository. Trivially, string names for registration can be created from the commandNames array. For an already allocated Plugin* p, the following code within pdCalc could implement registration:

```
const Plugin::PluginDescriptor& d = p->getPluginDescriptor();
for(int i = 0; i < d.nCommands; ++i)
CommandRepository::Instance().registerCommand(d.commandNames[i], MakeCommandPtr( d.commands[i]->clone() ));
```

At this point, you might recognize a dilemma with our plugins. Commands are allocated in a plugin, copied upon registration with the CommandRepository in the main program via a clone() call, and then ultimately deleted by the main program when
