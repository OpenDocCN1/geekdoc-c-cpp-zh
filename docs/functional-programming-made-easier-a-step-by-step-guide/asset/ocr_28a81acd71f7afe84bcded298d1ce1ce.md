```
```json
{ "tag": "QueryUsersRequest",
  "contents": {
    "authToken": "e0fc09ad-894a-4399-9940-870895c27394"
  }
}

{ "tag": "QueryUsersResponse",
  "contents": {
    "tag": "QueryUsersResultsSuccess",
    "contents": {
      "users": [
        { "tag": "User",
          "contents": {
            "userName": "joeuser",
            "temporaryPassword": true,
            "admin": true,
            "firstName": "Joe",
            "lastName": "Mama"
          }
        },
        { "tag": "User",
          "contents": {
            "userName": "janeuser",
            "temporaryPassword": false,
            "admin": false,
            "firstName": "Jane",
            "lastName": "Mama"
          }
        }
      ]
    }
  }
}

{ "tag": "QueryUsersResponse",
  "contents": {
    "tag": "QueryUsersResultsFailure",
    "contents": {
      "reason": { "tag": "NotAuthorized" }
    }
  }
}
```
```