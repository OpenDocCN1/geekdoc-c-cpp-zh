# Q.3 What is .net Remoting ?

Ans. : .NET Remoting is an enabler for application communication. It is a generic system for different applications to use to communicate with one another. .NET objects are exposed to remote processes, thus allowing interprocess communication. The applications can be located on the same comput

# Q.4 Define marshaling.

Ans. : The process of preparing an object to be remoted is called marshaling. On a single machine, objects might need to be marshaled across context, app domain or process boundaries.

# Q.5 What are channels in .NET remoting ?

Ans. : Channels represent the objects that transfer the other serialized objects from one application domain to another and from one computer to another, as well as one process to another on the same box. A channel must exist before an object can be transferred.

# Q.6 List the information stored in the configuration file for remoting.

AU : Dec-18

Ans. : Remoting configuration files, like other configuration files in .NET, are Extensible Markup Language (XML) files that use the .config extension. Configuration files can be used in remoting in lieu of source code creation and registration. In the examples so far, there hasn't been a desperate need for configuration files, but as one should get into customized sinks, the amount and complexity of code required to create and register remote objects increases dramatically. Configuration files also permit configuration changes without code changes.

The naming convention for remoting configuration files is the executable program name and extension, with a .config extension. Thus, for ClientActivatedServerExe.exe, the configuration file would be named ClientActivatedServerExe.exe.config. At this point, it should be evident that less wordy project names are a good idea! The location of the configuration file must be in the same directory as the executable file.

The configuration files are located in the Samples1 with the source files in the directories of the four executable files. They should be moved to the respective "bin/debug" directories. the server's configuration file, and like all .NET configuration files, the root element is <configuration>. Remoting configuration is placed in the subelement <system.runtime.remoting>. This is a configuration for a client-activated object. The <application> tag contains the optional name attribute that identifies the URI of the remote object. If the name attribute is dropped, the client's configuration tag, below, would have to be changed to <client url="tcp://localhost:1234">.