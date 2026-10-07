```
{
  "source": "",
  "miss": "never",
  {
    "source": ");"
  }
],
  "hits": 4,
  "miss": true
}
```

As you can see above, the miss is reported on the line and individual code branch, if there happens to be one. This allows the tool reading the JSON output to more easily parse and represent the missed code. Additionally, you can see the number of executions that hit this line, but ended up missing the code. Each line number is represented as the key name in the parent object. Each JSON entry starts with the code file information that coverage is checked against, which can be viewed here:

```
{
  "filename": "lib/payload.js",
  "percent": 92.59259259256,
  "hits": 25,
  "misses": 2,
  "sloc": 27,
  "source": {
    {
      "1": "",
      "miss": false
    }
  }
}
```

Additionally, the JSON reporter, like the 'html' reporter, includes information about individual tests executed. Every test name is displayed with execution duration and, most importantly, if the test passed or not. This part of the JSON output is shown below:

```
{
  "tests": {
    "request()": [
      {
        "title": "requests a resource with callback",
        "err": false,
        "duration": 23
      },
      {
        "title": "requests a POST resource",
        "err": false,
    }
  }
```