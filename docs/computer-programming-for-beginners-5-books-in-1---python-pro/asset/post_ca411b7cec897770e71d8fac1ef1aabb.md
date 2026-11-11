
```js
import {everywhere} from "./crow-tech";

everywhere(nest => {
  nest.state.gossip = [];
});

function sendGossip(nest, message, exceptFor = null) {
  nest.state.gossip.push(message);
  for (let neighbor of nest.neighbors) {
    if (neighbor == exceptFor) continue;
    request(nest, neighbor, "gossip", message);
  }
}

requestType("gossip", (nest, message, source) => {
  if (nest.state.gossip.includes(message)) return;
  console.log(`${nest.name} received gossip '${message}' from ${source}`);
  sendGossip(nest, message, source);
});
```

To avoid transmitting the same message across the network forever, every nest saves an array of gossip strings that it has seen. To describe this array, we use the everywhere function to run code on each nest that attaches a property to the nest’s state object.

## Message routing

If a given node wants to communicate with a single other node, the best approach is to build a path for messages to jump from node to node until they get to their destination. You need to understand the interface of the network. To send a request to a nest at a distance, it is important to know which neighboring nest can get the job done. Every nest knows about its direct neighbors only; it cannot compute a route, it lacks the information. You must understand how to spread the information about these connections to every nest in a way that enables it to transform with time, when new nests are created. Now you can use flooding, but instead of checking whether a message has been collected, now check if the new set of neighbors for a given nest is similar to the current set.

```js
requestType("connections", (nest, {name, neighbors}, source) => {
  let connections = nest.state.connections;
  if (JSON.stringify(connections.get(name)) == JSON.stringify(neighbors)) return;
  connections.set(name, neighbors);
  broadcastConnections(nest, name, source);
});

function broadcastConnections(nest, name, exceptFor = null) {
  for (let neighbor of nest.neighbors) {
    if (neighbor == exceptFor) continue;
    request(nest, neighbor, "connections", {
      name,
      neighbors: nest.state.connections.get(name)
    });
  }
}

everywhere(nest => {
  nest.state.connections = new Map;
  nest.state.connections.set(nest.name, nest.neighbors);
  broadcastConnections(nest, nest.name);
});
```

The comparison uses JSON.stringify because ==, on objects or arrays, will return true only when the values of the two are the same. Comparing the JSON strings is a very effective way to compare their content. The nodes instantly begin transmitting their connections except to unreachable nests, giving them a map of the existing network graph. The findRoute function finds a path to reach a given node within the network. But instead of sending back the whole route, it just brings back the next step. That next nest will use its existing information about the network to determine where to transfer the message.

```js
function findRoute(from, to, connections) {
  let work = [{at: from, via: null}];
  for (let i = 0; i < work.length; i++) {
    let {at, via} = work[i];
    for (let next of connections.get(at) || []) {
      if (next == to) return via;
      if (!work.some(w => w.at == next)) {
        work.push({at: next, via: via || next});
      }
    }
  }
  return null;
}
```

You can now create a function that can send messages over long distances. If the message is addressed to a direct neighbor, it is conveyed as usual. If not, it is wrapped in an object and transferred to a neighbor closer to the target, through the "route" request type, that will make that neighbor repeat the same operation.

```javascript
function routeRequest(nest, target, type, content) {
  if (nest.neighbors.includes(target)) {
    return request(nest, target, type, content);
  } else {
    let via = findRoute(nest.name, target, nest.state.connections);
    if (!via) throw new Error(`No route to ${target}`);
    return request(nest, via, "route", {target, type, content});
  }
}

requestType("route", (nest, {target, type, content}) => {
  return routeRequest(nest, target, type, content);
});
```

We have created different layers of functionality on top of a basic communication system to make it easier to use. This is a simplified model of how computer networks work.

## Async functions

To save important information, crows use the duplication method; they duplicate it across nests. That way, when a bird dismantles a nest, the information would not be lost. To recover a particular piece of information that has no local storage, a nest computer would talk to random other nests in the network until the one that has it is found.

```javascript
requestType("storage", (nest, name) => storage(nest, name));

function findInStorage(nest, name) {
  return storage(nest, name).then(found => {
    if (found != null) return found;
    else return findInRemoteStorage(nest, name);
  });
}

function network(nest) {
  return Array.from(nest.state.connections.keys());
}

function findInRemoteStorage(nest, name) {
  let sources = network(nest).filter(n => n != nest.name);

  function next() {
    if (sources.length === 0) {
      return Promise.reject(new Error("Not found"));
    } else {
      let source = sources[Math.floor(Math.random() *
        sources.length)];
      sources = sources.filter(n => n !== source);
      return routeRequest(nest, source, "storage", name)
        .then(value => value != null ? value : next(),
          next);
    }
  }

  return next();
}
```

Object.keys cannot work on connections because it is a Map. It contains a keys method, but that returns an iterator instead of an array. An iterator can be transformed to an array using the Array.from function. Various asynchronous actions are tied together in unclear ways. Now you need a recursive function to model looping across the nests. In a synchronous programming model, it is easy to express. JavaScript also lets you write pseudo-synchronous code to define asynchronous computation. An async function is a function that returns a promise and that can wait for other promises in a synchronous way. Rewrite findInStorage like this:

```javascript
async function findInStorage(nest, name) {
  let local = await storage(nest, name);
  if (local != null) return local;
  let sources = network(nest).filter(n => n != nest.name);
  while (sources.length > 0) {
    let source = sources[Math.floor(Math.random() *
      sources.length)];
    sources = sources.filter(n => n != source);
    try {
      let found = await routeRequest(nest, source, "storage",
        name);
      if (found != null) return found;
    } catch (_) {}
  }
  throw new Error("Not found");
}
```

An async function is marked with the word async and then the function keyword. Methods can also become async by writing async before their name. When the function or method is called, it returns a promise. When the body returns something, that promise is resolved. If it throws an exception, the promise is rejected. Within an async function, the word await is set in front of an expression to await a promise to settle and only then proceeds to execute the function. Such functions cannot run from start to finish at once, but they can be frozen at points and can restart later. For non-trivial asynchronous code, this notation is easier than working directly with promises.

## Generators

Async functions do not have to be paused and then resumed again. JavaScript has a feature called generator functions. These are similar but do not involve promises. When you call a function with function* (put an asterisk after the word function), it changes to a generator. When you call a generator, it returns an iterator.

```javascript
function* powers(n) {
  for (let current = n; ; current *= n) {
    yield current;
  }
}
```

```javascript
for (let power of powers(3)) {
  if (power > 50) break;
  console.log(power);
}
// → 3
// → 9
// → 27
```

Normally, if you call powers, the function is frozen at the beginning. Each time you call next on the iterator, the function will run until it hits a yield expression, which will pause it and make the yielded value the next value provided by the iterator. When the function returns, the iterator completes. Writing iterators is simple when you use generator functions. Write the iterator for the Group class with this generator:

```javascript
Group.prototype[Symbol.iterator] = function*() {
  for (let i = 0; i < this.members.length; i++) {
    yield this.members[i];
  }
};
```
