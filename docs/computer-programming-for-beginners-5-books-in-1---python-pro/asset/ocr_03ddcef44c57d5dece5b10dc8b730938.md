```
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
}
everywhere(nest => {
  nest.state.connections = new Map;
  nest.state.connections.set(nest.name, nest.neighbors);
  broadcastConnections(nest, nest.names);
});
```

The comparison utilizes JSON.stringify because ==, on objects or arrays, will send back true when the value of the two are the same only. Differentiating the JSON strings is a very successful way to compare their content. The nodes instantly begin transmitting their connections except to the unreachable nests, which give them a map of the existing network graph. The findRoute function finds a path to reach a set node within the network. But instead of sending back the whole route, it just brings back the next step. That next nest will use its existing information about the network, determine where it transfers the message.

```
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

You can now create a function that can send messages to long distance. If the