```
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
```