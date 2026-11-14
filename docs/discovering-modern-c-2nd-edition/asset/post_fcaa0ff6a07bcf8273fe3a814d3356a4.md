
This example allows us to show a realistic application, and we assume that many scientists and engineers have to deal with databases from time to time. Although the Oracle database is a commercial product, our example can be tested with the free Express edition. Furthermore, this technique can also be applied to other old-fashioned software libraries.

OCCI is a C++ extension of the C library OCI and adds only a very thin layer with some features on top while keeping the entire software architecture in C style. Sadly, this applies to many inter-language interfaces of C libraries. Since C does not support destructors, one cannot establish RAII and resources must be released manually.

In OCCI, we first have to create an `Environment` which can be used to establish a `Connection` to the database. This in turn allows us to write a `Statement` that returns a `ResultSet`. All these resources are represented by raw pointers and must be released in reverse order.

## Table 2–1: Herbert’s Solutions

| Problem | Worth an Award |
|---|---|
| Gauss circle | ✓ |
| Congruent numbers | ? |
| Amicable numbers | ✓ |
| ... | |

As an example, we look at Table 2–1 where our friend Herbert keeps track of his solutions to (allegedly) unsolved mathematical problems. The second column indicates whether he is certain to deserve an award for his work. For size reasons, we cannot print the complete list of his tremendous discoveries here.

```
=> c++03/occi_old_style.cpp
```

From time to time, Herbert looks up his award-worthy discoveries with the following C++ program:

Click here to view code image

```cpp
#include <iostream>
#include <string>
#include <occi.h>

using namespace std;          // import names (§3.2.1)
using namespace oracle::occi;

int main()
{
    string dbConn= "172.17.42.1", user= "herbert",
           password= "NSA_go_away";
    Environment *env = Environment::createEnvironment();
    Connection *conn = env->createConnection(user, password,
                                             dbConn);

    string query= "select problem from my_solutions"
                  " where award_worthy = 0";
    Statement *stmt = conn->createStatement(query);
    ResultSet *rs = stmt->executeQuery();

    while (rs->next())
        cout << rs->getString(1) << endl;

    stmt->closeResultSet(rs);
    conn->terminateStatement(stmt);
    env->terminateConnection(conn);
    Environment::terminateEnvironment(env);
}
```

This time, we cannot blame Herbert for his old-style programming; it is forced by the library. Let us have a look at the code. Even for people not familiar with OCCI, it is evident what happens. First we acquire the resources, then we iterate over Herbert’s ingenious achievements, and finally we release the resources in reverse order. We highlighted the resource release operations as we will have to pay closer attention to them.

The release technique works reasonably well when our (or Herbert’s) program is a monolithic block as above. The situation changes entirely when we try building functions with queries:

Click here to view code image

```
ResultSet *rs = makes_me_famous();
while (rs->next())
    cout << rs->getString(1) << endl;

ResultSet *rs2 = needs_more_work();
while (rs2->next())
    cout << rs2->getString(1) << endl;
```

Now we have result sets without the corresponding statements to close them; they were declared within the query functions and are out of scope now. Thus, for every object we have to keep additionally the object that was used for its generation. Sooner or later this becomes a nightmare of dependencies with an enormous potential for errors.

=> c++11/occi_resource_rescue.cpp

The question is: How can we manage resources that depend on other resources? The solution is to use deleters from shared_ptr. They are called whenever managed memory is released. An interesting aspect of deleters is that they are not obliged to actually release the memory. We will explore this liberty to manage our resources. The Environment has the easiest handling because it does not depend on another resource:

Click here to view code image

```cpp
struct environment_deleter {
    void operator()( Environment* env )
    { Environment::terminateEnvironment(env); }
};

shared_ptr<Environment> environment(
    Environment::createEnvironment(), environment_deleter());
```

Now, we can create as many copies of the environment as we like and have the guarantee that the deleter executing terminateEnvironment(env) is called when the last copy goes out of scope.

A Connection requires an Environment for its creation and termination. Therefore, we keep a copy in connection_deleter:

Click here to view code image

```cpp
struct connection_deleter
{
    connection_deleter(shared_ptr<Environment> env)
    : env(env) {}
    void operator()(Connection* conn)
    { env->terminateConnection(conn); }
    shared_ptr<Environment> env;
};
```

```cpp
shared_ptr<Connection> connection(
    environment->createConnection(...),
    connection_deleter(environment));
```

Now, we have the guarantee that the Connection is terminated when it is not needed any longer. Having a copy of the Environment in the connection_deleter ensures that it is not terminated as long as a Connection exists. We can also handle the database more conveniently when we create a manager class for it:

Click here to view code image

```cpp
class db_manager
{
public:
    using ResultSetSharedPtr = std::shared_ptr<ResultSet>;

    db_manager(string const& dbConnection, string const& dbUser,
               string const& dbPw)
        : environment(Environment::createEnvironment(),
                      environment_deleter{}),
          connection(environment->createConnection(dbUser, dbConnection),
                     connection_deleter{environment})
        {}
        // some getters ...
private:
    shared_ptr<Environment> environment;
    shared_ptr<Connection> connection;
};
```

Note that the class has no destructor since the members are managed resources now. To this class, we can add a query method that returns a managed ResultSet:

Click here to view code image

```cpp
struct result_set_deleter
{
    result_set_deleter(shared_ptr<Connection> conn,
                       Statement* stmt)
    : conn(conn), stmt(stmt) {}
    void operator()( ResultSet *rs ) // call op. like in §3.7
    {
        stmt->closeResultSet(rs);
        conn->terminateStatement(stmt);
    }
    shared_ptr<Connection> conn;
    Statement* stmt;
};
```

```cpp
class db_manager
{
public:
    // ...
    ResultSetSharedPtr query(const std::string& q) const
    {
        Statement *stmt= connection->createStatement(q);
        ResultSet *rs = stmt->executeQuery();
        auto deleter= result_set_deleter(connection, stmt);
        return ResultSetSharedPtr(rs, deleter);
    }
};
```

Thanks to this new method and our deleters, the application becomes as easy as:

Click here to view code image

```cpp
int main()
{
    db_manager db("172.17.42.1", "herbert", "NSA_go_away");
    auto rs= db.query("select problem from my_solutions "
                      " where award_worthy != 0");
    while (rs->next())
        cout << rs->getString(1) << endl;
}
```

The more queries we have, the more our effort pays off. Not being ashamed to repeat ourselves: all resources are implicitly released.

The careful reader has realized that we violated the single-responsibility principle. To express our gratitude for this discovery we invite you to improve our design in Exercise 2.8.5.

## 2.5 Method Generation Summary

C++ has six methods (four in C++03) that the compiler attempts to generate implicitly:

- Default constructor
- Copy constructor
- Move constructor (C++11 or higher)
- Copy assignment
- Move assignment (C++11 or higher)
- Destructor

This saves us from boring routine work and thus preventing oversights.

C++11 Since C++11, we can control (and document) this generation with the declarators default and delete:

Click here to view code image

```cpp
class complex
{
public:
    complex(const complex&) = delete;
    complex& operator=(const complex&) = default;
};
```

In this example, we deleted the copy constructor and requested the compiler to generate the copy assignment in the default manner (calling the copy assignments of all base classes and members). The implicit generation can silently omit one or more of the six methods from our list according to the rules in §A.5, whereas requesting the default generation of a certain method leads to a compiler error when this method cannot be generated. 15 The declarator delete is not limited to methods with implicit generation but can be applied to any function (illustrated for instance in Section 2.6.4). In C++03 we could not delete functions but could at least disable methods by declaring them in a private section. delete is a better way of expressing our intention which manifests in less-confusing error messages. In contrast to the private hack, we can use delete for free functions.
