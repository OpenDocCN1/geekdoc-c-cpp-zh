```
stmt->closeResultSet(rs);
conn->terminateStatement(stmt);
env->terminateConnection(conn);
Environment::terminateEnvironment(env);
}
```

This time, we cannot blame Herbert for his old-style programming; it is forced by the library. Let us have a look at the code. Even for people not familiar with OCCI, it is evident what happens. First, we acquire the resources, then we iterate over Herbert's ingenious achievements, and finally we release the resources in reverse order. We highlighted the resource release operations as we will have to pay closer attention to them.

The release technique works reasonably well when our (or Herbert's) program is a monolithic block as above. The situation changes entirely when we try building functions with queries:

```
ResultSet *rs = makes_me_famous();
while (rs->next())
  cout << rs->getString(1) << endl;

ResultSet *rs2 = needs_more_work();
while (rs2->next())
  cout << rs2->getString(1) << endl;
```

Now we have result sets without the corresponding statements to close them; they were declared within the query functions and are out of scope now. Thus, for every object we have to keep additionally the object that was used for its generation. Sooner or later this becomes a nightmare of dependencies with an enormous potential for errors.

```
=> c++11/ocl_resource_rescue.cpp
```

The question is: How can we manage resources that depend on other resources? The solution is to use deleters from unique_ptr or shared_ptr. They are called whenever managed memory is released. An interesting aspect of deleters is that they are not obliged to actually release the memory. We will explore this liberty to manage our resources. The Environment has the easiest handling because it does not depend on another resource:

```
struct environment_deleter {
  void operator() (Environment* env)
  { Environment::terminateEnvironment(env); }
};
```

```
shared_ptr<Environment> environment(
  Environment::createEnvironment(), environment_deleter{});
```

Now, we can create as many copies of the environment as we like and have the guarantee that the deleter executing terminateEnvironment(env) is called when the last copy goes out of scope.