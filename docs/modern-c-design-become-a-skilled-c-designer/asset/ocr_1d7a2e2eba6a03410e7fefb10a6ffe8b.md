descriptor by overriding the getPluginDescriptor() function, and let pdCalc register the commands. Since Commands must each implement a clone() function, pdCalc can copy the plugin command prototypes via this virtual function to register them with the CommandRepository. Trivially, string names for registration can be created from the commandNames array. For an already allocated Plugin* p, the following code within pdCalc could implement registration:

```
const Plugin::PluginDescriptor& d = p->getPluginDescriptor();
for(int i = 0; i < d.nCommands; ++i)
CommandRepository::Instance().registerCommand(d.commandNames[i], MakeCommandPtr( d.commands[i]->clone() ));
```

At this point, you might recognize a dilemma with our plugins. Commands are allocated in a plugin, copied upon registration with the CommandRepository in the main program via a clone() call, and then ultimately deleted by the main program when