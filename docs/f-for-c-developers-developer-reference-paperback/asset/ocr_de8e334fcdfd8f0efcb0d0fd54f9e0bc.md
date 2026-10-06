# LISTING 6-125 Merging and converting the event

```
// define an event
let myEvent = Event<int>()

// depending on the value, the event will be given a different label
let evenNumEvent, oddNumEvent =
    myEvent.Publish
    |> Observable.partition(fun n -> n % 2 = 0)

let merged = Observable.merge evenNumEvent oddNumEvent
merged
|> Observable.map float
|> Observable.add(fun floatValue -> printf("got value %f" floatValue))

// set even-number event handler
evenNumEvent.Add(fun i -> printf("even number %d triggered event" i))

// set odd-number event handler
oddNumEvent.Add(fun i -> printf("odd number %d triggered event" i))

//fire 5 events with arguments from 1 to 5
[1..5]
|> Seq.iter myEvent.Trigger

Execution result
got value 1.000000
odd number 1 triggered event
got value 2.000000
even number 2 triggered event
got value 3.000000
odd number 3 triggered event
got value 4.000000
even number 4 triggered event
got value 5.000000
odd number 5 triggered event
```

If you compare the sample code here and the code in the Seq module, they are very similar. As mentioned a few times in this section, the Observable module makes the event processing pretty much like data processing. The reason I've mentioned it a few times is this is something that other .NET languages do not provide without help from other libraries.