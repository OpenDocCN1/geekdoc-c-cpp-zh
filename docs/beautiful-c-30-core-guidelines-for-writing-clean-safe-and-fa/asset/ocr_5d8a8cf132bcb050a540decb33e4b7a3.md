```
std::string query;
};
```

The class is constructed with the server query. A call to population will check the expiry time of the population value and update it using the query if necessary. This lazy evaluation is a typical use case of mutable.

Bryn writes the constructor:

Click here to view code image

```
population_service::population_service(std::string query_)
{
    query = std::move(query_);
    expiry = std::chrono::system_clock::to_time_t(

    std::chrono::system_clock::now());
    current_population = population();
}
```

The population function is a simple matter. All the tests pass, and Bryn submits it for code review. He is asked to migrate initialization out of the constructor body and into the initialization list. Keen to make a good impression, Bryn turns this around in short order and produces this:

Click here to view code image

```
population_service::population_service(std::string query_)
    : query(std::move(query_))
    , expiry(std::chrono::system_clock::to_time_t(

    std::chrono::system_clock::now()))
    , current_population(population())
{}
```