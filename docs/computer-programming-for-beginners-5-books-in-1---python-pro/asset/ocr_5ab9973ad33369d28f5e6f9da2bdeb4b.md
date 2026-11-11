some other format when it is published. During a transitional period, use two separate module systems side by side.

# Module design

Program structuring is one of the nice features of programming. Any unknown functionality can model in different ways. The good program design is a personalized one, and there is a matter of preference and taste. To understand the value of well-organized design, you need to read and work on several programs and take note of performing and non-performing functions. The module design is straightforward to use. The ini package module follows the standard JSON object by supplying stringify and parse (to write an INI file) functions, and, like JSON, changes between plain objects and strings. A lot of the INI-file parsing modules on NPM supply a function that reads that type of file from the hard disk and parses it. Concentrated modules that calculate values are suitable in a larger range of programs than larger modules that execute complex actions that have side effects. An INI file reader that want to read the file from disk is not useful in cases whereby the file’s content comes from another source. Similarly, stateful objects are occasionally necessary and useful, but if you can use a function, utilize it. Various INI file readers on NPM gives a layout style that needs you to build an object, then load the file into the object, and use specific methods to achieve the desired results. It is the object-oriented style and tradition. In JavaScript, there is no particular way to represent a graph. There are various pathfinding packages available on NPM, but none utilizes the graph format. They often let graph edges contain a weight, and that is the distance or cost-related with it. For instance, we have the dijkstrajs package. A recognized way to pathfinding, related to the findRoute function is the Dijkstra’s algorithm, after Edsger Dijkstra, the package first writer. The js suffix is regularly attached to package names to specify that you can write in JavaScript. So, if you want to use that package, ensure that the graph saves in its expected format.

```
const {find_path} = require("dijkstrajs");
let graph = {};
for (let node of Object.keys(roadGraph)) {
  let edges = graph[node] = {};
  for (let dest of roadGraph[node]) {
    edges[dest] = 1;
  }
}
console.log(find_path(graph, "Post Office", "Cabin"));
// → ["Post Office", "Alice's House", "Cabin"]
```