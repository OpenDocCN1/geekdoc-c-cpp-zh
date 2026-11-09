![](bbox=[0.24, 0.08, 0.7, 0.44])

Every query, update, delete, or add we want to perform in the database will have a corresponding method in a `Gateway` interface. There can, of course, be many `Gateways`, depending on how we want to partition the database.

The `GatewayImpl` class implements the gateway and directs the actual database to perform the functions required. If this is a SQL database, then all the SQL is created within the `GatewayImpl` class. If you are using ORM, the ORM framework is manipulated by the `GatewayImpl` class. Neither SQL nor the ORM framework nor the database API is known above the architectural boundary that separates the `Gateway` from the `GatewayImpl`¹.

Indeed, we don’t even want the schema of the database known above that boundary. The `GatewayImpl` should unpack the rows, or data elements, retrieved from the database and use that data to construct appropriate business objects to pass across the boundary to the business rules.

And now testing the database is trivial. You create a suitably simple test database, and then you call each query function of the `GatewayImpl` from your tests and ensure that it has the desired effect on that test database. Make sure that each query function returns a properly loaded set of business