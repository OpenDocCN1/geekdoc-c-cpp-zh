```
```javascript
function randomRobot(state) {
  return {direction: randomPick(roadGraph[state.place])};
}
```
```

If you want to test this unique robot, create a new state with few parcels.

```
```javascript
VillageState.random = function(parcelCount = 5) {
  let parcels = [];
  for (let i = 0; i < parcelCount; i++) {
    let address = randomPick(Object.keys(roadGraph));
    let place;
    do {
      place = randomPick(Object.keys(roadGraph));
    } while (place == address);
    parcels.push({place, address});
  }
  return new VillageState("Post Office", parcels);
};
```
```

The do loop continues to select new places when it gets a correct address. Let’s start up a virtual world.

```
```javascript
runRobot(VillageState.random(), randomRobot);
// → Advances to Marketplace
// → Advances to Town Hall
// → …
// → Run in 63 turns
```
```

It takes the robot too many turns to transport the parcels because there was no plan ahead.

# ### The mail truck's route

If you search a route that goes through all the places in the village, that could run twice by the robot, but there is a guarantee it will run it. Below is an example: (starting from the post office):

```
```javascript
const mailRoute = [
  "Alice's House", "Cabin", "Alice's House", "Bob's House",
  "Town Hall", "Daria's House", "Ernie's House",
  "Greta's House", "Shop", "Greta's House", "Farm",
  "Marketplace", "Post Office"
];
```
```

To use the route, you need to utilize the robot memory. The rest of the robot route is stored in its memory and dispatches the first element at every turn.

```
```javascript
function routeRobot(state, memory) {
```
```