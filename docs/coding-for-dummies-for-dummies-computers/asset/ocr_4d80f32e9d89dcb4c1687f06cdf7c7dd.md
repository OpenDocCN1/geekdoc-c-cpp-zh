# What do APIs do?

An API allows Program A to access select functions of another separate Program B. Program B grants access by allowing Program A to make a data request in a structured, predictable, documented way, and Program B responds to this data request with a structured, predictable, documented response, as follows (see Figure 9-7):

+   - **It’s structured** because the fields in the request and the data in the response follow an easy-to-read standardized format. For example, the Yahoo Weather API data response includes these selected structured data fields:

```
```json
"location": {
    "city": "New York",
    "region": "NY"
},
"units": {
    "temperature": "F"
},
"forecast": [
    {
        "date": "29 Oct 2014",
        "high": "68",
        "low": "48",
        "text": "PM Showers"
    }
]
```
```

See the full Yahoo Weather API response by visiting `http://developer.yahoo.com/weather/`.

+   - **It’s predictable** because the fields that must be included and can be included in the request are pre-specified, and the response to a successful request will always include the same field types.

+   - **It’s documented** because the API is explained in detail. Any changes usually are communicated through the website, social media, email, and even after the API changes, there is often a period of backward compatibility when the old API requests will receive a response. For example, when Google Maps issued version 3 of their API, version 2 still operated for a certain grace period.

![](bbox=[0.23, 0.768, 0.64, 0.881])

**Figure 9-7:** An API allows two separate programs to talk to each other.