# # Extract Field

This refactoring can have a profoundly positive effect. I don’t use it often, but when I do, it puts the code on a path to substantial improvement.

It all begins with a failed **Extract Method**. Consider the following class, which converts a CSV file of data into a report. It’s a bit of a mess.

[Click here to view code image](#)

```
```java
public class NewCasesReporter {
    public String makeReport(String countyCsv) {
        int totalCases = 0;
        Map<String, Integer> stateCounts = new HashMap<>();
        List<County> counties = new ArrayList<>();


        String[] lines = countyCsv.split("\n");
        for (String line : lines) {
            String[] tokens = line.split(",");
            County county = new County();
            county.county = tokens[0].trim();
            county.state = tokens[1].trim();
            //compute rolling average
            int lastDay = tokens.length - 1;
            int firstDay = lastDay - 7 + 1;
            if (firstDay < 2)
                firstDay = 2;
            double n = lastDay - firstDay + 1;
            int sum = 0;
            for (int day = firstDay; day <= lastDay; day++)
                sum += Integer.parseInt(tokens[day].trim());
            county.rollingAverage = (sum / n);


            //compute sum of cases.
            int cases = 0;
            for (int i = 2; i < tokens.length; i++)
                cases += (Integer.parseInt(tokens[i].trim()));
            totalCases += cases;
            int stateCount = stateCounts.getOrDefault(county.state, 0);
            stateCounts.put(county.state, stateCount + cases);
            counties.add(county);
        }
        StringBuilder report = new StringBuilder("" +
```
```