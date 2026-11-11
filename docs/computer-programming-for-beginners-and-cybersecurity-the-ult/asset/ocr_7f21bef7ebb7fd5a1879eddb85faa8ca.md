ReplaceAll() uses a UnaryOperator as its functional interface, which is a Function sub interface.

Both replaceIf() and replaceAll() are available to all subclasses with one caveat: the underlying class must support removal, or an exception will be thrown.

These examples show the compactness of functional programming. Most of the work was done by the function with the lambda providing the details.

# Map interface

One of the biggest irritants of using lists as values in maps is the constant need to check for the presence of the map before adding, updating, or removing an element. First, you must try to extract the list and create it if it is not found. For example, say we have a method that updates a movie database implemented as a Map. The map’s key is the year of the movie, and its value is a list of movies for that year. Pre-Java 8, the code would look like this:

```
```java
private Map<Integer, List<String>> movieDatabase = new HashMap<>();

private void addMovie(Integer year, String title) {
    List<String> movies = movieDatabase.get(year);

    if (movies == null) {
        // Need to create the array list if it doesn't yet exist
        movies = new LinkedList<String>();
        movieDatabase.put(year, movies);
    }

    movies.add(title);
}
```
```

Java 8 offers a better alternative with these default methods: