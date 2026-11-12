```
```java
@Override
public Object getItem(int position) {
    if(data==null)
        return null;
    try{
        JSONObject element = (JSONObject)data.get(position);
        return element;
    }catch(Exception e){
        return null;
    }
}
@Override
public long getItemId(int position) {
    return position;
}
```
```

This code, for the most part, wraps accessors to the JSON object. It handles getting an item from a position (which in this example is the index into the JSON array). If no data has been set, then the Adapter simply reports that there's nothing to see. The only method in the example that doesn't override a required function is the code that changes the data set. It also calls notifyDataSetChanged and, as a result of this method, must be called on the main thread. My class extends from BaseAdapter because it contains all the baseline methods that I need to build my custom adapter.