He submits it and gets a knock on the door from his lead, Beth.
“Bryn,” she asks, “did you test this?”
“Yup, all green,” he answers, innocently.
“Did you test this AFTER you migrated everything to the initialization list?” she persists.
“Well, there was no need, was there?” he responds. “I’ve just moved everything before the braces.”
Beth dies a little on the inside. In her mind she is preparing the “automate your tests and always test prior to submission” lecture in the face of this answer. She did not need to run the code to see that there was a problem.

Unfortunately, moving everything up changes the behavior of the code. The first thing that happens now is that current_population is initialized by a call to popula-tion. Setting aside the questionable wisdom of calling a member function from an initializer list, this was not the original intent of the engineer. He wanted to initialize the query and the expiry time first. Without those values correctly initialized, the call to population is vanishingly unlikely to succeed.

To be absolutely clear, member data is initialized in order of declaration. That is the only order. There is no magical choosing going on, nor is there any variation available to you. In this case, current_population was declared first, so that was ini-tialized by the call to the member function population. The expiry member was ini-tialized next, but std::time_t has no constructor and usually consists of a built-in integral type, so it was not initialized to a deterministic value. Finally, query was ini-tialized by move construction.

There are two ways to fix the problem. The correct way to initialize this object is to initialize current_population to zero and expiry to now(), and then move-construct the query, thus:

Click here to view code image

```
population_service::population_service(std::string query_)
  : current_population(0)
  , expiry(std::chrono::system_clock::to_time_t(
```