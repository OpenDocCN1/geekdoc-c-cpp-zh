# Fetch your recent tweets.

The following code relies on Prototype for a few things ($(), each(), escapeHTML(), insert()...) but is readily convertible to other frameworks.

```
```javascript
var REGEXP_URL = new RegExp('https?://(.)*?(\W?|\s|$)'
```

# Check out part of a JSON-encoded tweet.

(Actual returned datasets are far more detailed, and URLs are obviously not truncated—this is just to give you an idea.)

```
```json
{
  "in_reply_to_screen_name": null,
  "user": {
    "friends_count": 27, "statuses_count": 622,
    "name": "Christophe Porteneuve",
    "followers_count": 215,
    "profile_image_url": "http://a3.twimg.com/.../headshot_tdd_normal.jpg"
  },
  "id": 9531762839, "created_at": "Tue Feb 23 18:35:22 +0000 2010",
  "in_reply_to_status_id": null,
  "text": "15' pour 850m. Sympa av Saint-Ouen + av Clichy aux heures de..."
}
```
```