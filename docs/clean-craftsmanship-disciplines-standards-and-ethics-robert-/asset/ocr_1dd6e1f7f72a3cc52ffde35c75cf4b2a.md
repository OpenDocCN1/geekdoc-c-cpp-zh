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
```
```