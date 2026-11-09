```
```java
public class NewCasesReporterTest {
    private final double DELTA = 0.0001;
    private NewCasesReporter reporter;

    @Before
    public void setUp() throws Exception {
        reporter = new NewCasesReporter();
    }

    @Test
    public void countyReport() throws Exception {
        String report = reporter.makeReport("" +
            "c1, s1, 1, 1, 1, 1, 1, 1, 7\n" +
            "c2, s2, 2, 2, 2, 2, 2, 2, 7");
        assertEquals("" +
            "County    State    Avg New Cases\n" +
            "======    =====    =============\n" +
            "c1        s1       1.86\n" +
            "c2        s2       2.71\n\n" +
            "s1 cases: 14\n" +
            "s2 cases: 21\n" +
            "Total Cases: 35\n",
            report);
    }
}
```
```