```
}
console.log(tableFor("pizza", JOURNAL));
// → [76, 9, 4, 1]
```

Arrays consists of an include method, which is used to check if a set value exists in the array. This method is used by the function to decide if the event name is interested the stated event list for a given day.

# Array loops

The tableFor function contains a loop like this:

```
for (let I = 0; I < JOURNAL.length; I++) {
  let entry = JOURNAL[i];
  // Do something with entry
}
```

This type of loop is used in high-level JavaScript
This is how to write that type of loop in modern JavaScript.

```
for (entrance of JOURNAL) {
  console.log(`${entrance.events.length} events.`);
}
```

With a loop like this, the loop continues across the elements of the value specified after of. This loop is used for strings and other data layouts.

# The final analysis

A correlation is calculated for every type of event that happens in the data set. If you want to achieve that, search every type of event.

```
function journalEvents(journal) {let events = [];
  for (let entry of journal) {
    for (let event of entry.events) {
      if (!events.includes(event)) {
        events.push(event);
      }
    }
  }
  return events;
}

console.log(journalEvents(JOURNAL));
// → ["carrot", "exercise", "weekend", "bread", …]
```

By moving across every event and making additions to those that are not in the events array, this function gathers all the type of event.

A lot of correlations appear to lie close to zero. Eating bread, carrots or pudding does not activate the squirrel-lycanthropy. It happens often during the weekends.