# Chapter 2.4

# C.47: Define and initialize member variables in the order of member declaration

There is only one order of initialization of member data, which is the order of declaration. You cannot change this. There are very good reasons for this being an immutable rule, which we will describe in this chapter.

But first, an example. Bryn, a new engineer at a large firm, is asked to write a population service for finding out how many people are in the building. A server locked away in the bowels of the building handles admissions and exits. It is old and slow. Etched on the front in red lettering is the name of a forgotten hardware company long ago sold to a rapacious and overfunded startup. Queries are rather cumbersome and time consuming. New safety regulations require the number to be available instantaneously, but since it takes about a minute for someone to sign in at the front desk it is considered safe to query the server, cache the value, and retain it for 30 seconds. This will stop queries from building up faster than they can be handled.

I know you’re laughing. This is a true story, although I have changed the names. Bryn produces this simple solution:

Click here to view code image

```
class population_service {
public:
    population_service(std::string query);
    float population() const;

private:
    mutable float current_population;
    mutable std::time_t expiry;
}
```