```
class Util {
    public static int Min(int[] paramList) {
        // Verify that the caller has provided at least one parameter.
        // If not, throw an IllegalArgumentException - it is not possible
        // to find the smallest value in an empty list.
        if (paramList == null || paramList.length == 0) {
            throw new IllegalArgumentException("Utils.Min: not enough arguments");
        }

        // Set the current minimum value found in the list of parameters to the first item.
        int currentMin = paramList[0];

        // Iterate through the list of parameters, searching to see whether any of them
        // are smaller than the value held in currentMin.
        foreach (int i : paramList) {
            // If the loop finds an item that is smaller than the value held in
            // currentMin, then set currentMin to this value.
            if (i < currentMin) {
                currentMin = i;
            }
        }

        // At the end of the loop, currentMin holds the value of the smallest
        // item in the list of parameters, so return this value.
        return currentMin;
    }
}
```