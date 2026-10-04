# Get Your ViewModel On 635

# MVVM? ViewModel? Who's on first?

Several versions of ViewModel are floating around, and an equal number of "frameworks." They all seem to have slightly different names and implementations. This is largely because MVVM is a recently created pattern (as patterns), and there are quite a few people trying to make "their" name stick. In fact, the name doesn't matter as much as the benefit received. This book uses the name ViewModel because that is where the dart hits the wall.

My recommendation is to look at all the different flavors of user interface patterns, the parts that you work best in your vision, and throw out the parts that don't make sense. Patterns are meant to spark critical thought, not be considered as absolutes.

The ViewModel pattern presented in this book has been working extremely well for my customers in both large and small applications and is not meant to be an exact blueprint.

Practical WPF

“Won't it take longer to develop an application using one of these patterns?” That is a common question, and the answer is very simple, "It depends." Once developers fully understand the objectives and techniques, *velocity* (the amount of work accomplished by a team in a given period of time) starts catching up. Getting to that level of understanding (especially if several variations are attempted) can take time and usually involves a bit of thrashing along the way.

When there is a change request (users call them bugs, but I prefer a different nomenclature). If you're using a presentation pattern that ensures separation of concerns, it is clear where to go in the codebase to resolve the issue. Traditional development styles (like those techniques commonly used in Windows Forms) make it all too easy to place business code into event handlers and code-behind files, mixing concerns and dependencies.

# Traditional!

To fully understand why the ViewModel pattern helps, you need to understand the stands of a "traditional" application architecture.

# Data Access Layer (DAL)

The DAL is the set of classes and methods that get the data out of the data store (such as SQL Server) and populate the Model (see next item). It is also responsible for persisting (saving) any changes to the data back to the data store.

# Model

The Model is the data that composes your application — not the data store itself (for example, the database), but the object graph (see WikiPedia,