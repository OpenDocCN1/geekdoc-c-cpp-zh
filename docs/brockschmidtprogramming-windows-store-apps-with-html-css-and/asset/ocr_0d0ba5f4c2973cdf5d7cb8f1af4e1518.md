```
```js
return decode(j.number);
}

//"this" will be bound to the list that's being grouped
function decodeGroupData(j) {
    var dec = decode(j.number);

    //Do a quick in-place filtering of the list so we can get the population of the decade.
    var decArray = this.filter(function (v) { return (decode(v.number) == dec); });

    return {
        decade: dec,
        name: dec.toString(),
        count: decArray.length
    }
}
```
```

Full list grouped by decades: [colored decade blocks]

```
```
Group data:
{"decade":0,"name":"0","count":4}
{"decade":10,"name":"10","count":1}
{"decade":20,"name":"20","count":1}
{"decade":30,"name":"30","count":2}
{"decade":40,"name":"40","count":2}
{"decade":50,"name":"50","count":1}
{"decade":60,"name":"60","count":1}
{"decade":80,"name":"80","count":5}
{"decade":90,"name":"90","count":3}
```
```

And a last one that's grouped by decades with the groups sorted in descending order, using the same key and group data functions as above:

```
```js
this._groupedByDecadesSortedByCount =
    this._list.createGrouped(decadeKey, decodeGroupData.bind(this._list),
        //j and k are keys as returned from decadeKey; k>j does reverse sort
        function (j, k) { return k - j; });
```
```

Full list grouped by decades, reverse sorted [colored decade blocks]

```
```
Group data:
{"decade":90,"name":"90","count":3}
{"decade":80,"name":"80","count":5}
{"decade":60,"name":"60","count":1}
{"decade":50,"name":"50","count":1}
{"decade":40,"name":"40","count":2}
{"decade":30,"name":"30","count":2}
{"decade":20,"name":"20","count":1}
{"decade":10,"name":"10","count":1}
{"decade":0,"name":"0","count":4}
```
```