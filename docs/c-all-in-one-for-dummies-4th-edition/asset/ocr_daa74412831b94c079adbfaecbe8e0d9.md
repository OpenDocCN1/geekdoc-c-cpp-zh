# Considering the nesting scenario issues

In the classes you’re creating, you want to make the task easy on your coworkers. In doing so, you may make a primary class, such as `EthicalCompetition`, that they will instantiate to use your set of classes. This primary class will include the methods for using the system. In other words, it serves as an *interface* to the set of classes.

In addition to the main `EthicalCompetition` class, you might create additional auxiliary classes that the `EthicalCompetition` class will use, but your coworkers won’t interact with directly. One might be a class called `Connection` that handles the tasks of connecting to the competitor’s computer. However, the `Connection` class may present these problems:

+   - **Potential conflicts:** The class `Connection` may be something you write, but your organization may support another `Connection` class, and your coworkers might need to use that class.
+   - **Privacy:** You may not want your coworkers using this special `Connection` class. Perhaps it has special functionality that would reveal too many organizational secrets, or you just want them using the main interface, the `EthicalCompetition` class.

To solve the unique name problem, you have several choices. For one, you can just rename the class something different, such as `EthicalCompetitionConnection`. But that’s a bit long for a class used exclusively for internal needs. However, you could shorten the class name and call it something that’s likely to be unique, such as `ECConnection`.

Yet at the same time, if the users of your classes look at the header file and see a whole set of classes, which classes they should be using may not be clear. (Of course, you would write some documentation to clear this up, but you do want the code to be at least somewhat self-explanatory.)

# Understanding the nested class solution

One solution for dealing with both naming conflict and privacy issues for support classes is to use *nested classes*. With a nested class, you write the declaration for the main class, `EthicalCompetition`, and then, inside the class, you write the supporting classes, as in the following:

```
class EthicalCompetition {
private:
  class Connection {
  public:
```