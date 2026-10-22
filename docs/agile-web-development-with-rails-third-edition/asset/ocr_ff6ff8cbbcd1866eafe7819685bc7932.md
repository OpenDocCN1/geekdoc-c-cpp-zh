# 3.5 Choosing a Rails Version

The previous instructions helped you install the latest version of Rails. But occasionally you might not want to run with that version. Perhaps a new version of Rails has come out since this book has been published, so you want to be absolutely confident that the examples that you see here exactly match the version of Rails you are running. Or perhaps you are developing on one machine but intending to deploy on another machine that contains a version of Rails that you don’t have any control over.

If either of these situations applies to you, you need to be aware of a few things. For starters, you can find out all the versions of Rails you have installed using the gem command:

```
gem list --local rails
```

You can also verify what version of Rails you are running as the default by using the rails --version command. It should return 2.2.2 or later.

Installing another version of Rails is also done via the gem command. Depending on your operating system, you might need to preface the command with sudo.

```
gem install rails --version 2.2.2
```

Now, having multiple versions of Rails wouldn’t do anybody any good unless there were a way to pick one. As luck would have it, there is. On any rails command, you can control which version of Rails is used by inserting the full version number surrounded by underscores before the first parameter of the command:

```
rails _2.2.2_ --version
```

This is particularly handy when you create a new application, because once you create an application with a specific version of Rails, it will continue to use that version of Rails—even if newer versions are installed on the system—until you decide it is time to upgrade. How to change the version of Rails that your application is using is described in the sidebar on page 264.

And finally, should you decide to proceed using a version other than 2.2.2, you are not completely on your own. You can find a list of changes that will affect you at http://wiki.pragprog.com/changes-to-rails.

# 3.6 Development Environments

The day-to-day business of writing Rails programs is pretty straightforward. Everyone works differently: here’s how we work.