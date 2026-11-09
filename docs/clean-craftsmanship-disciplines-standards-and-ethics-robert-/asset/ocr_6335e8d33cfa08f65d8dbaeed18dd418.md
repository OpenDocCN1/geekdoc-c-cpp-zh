```
```java
// T: 14:07 Stack.java
public void push(int element) {
    this.elements[size++] = element;
}

public class PrimeFactorsTest {
    @Test
    public void factors() throws Exception {
        assertThat(factorsOf(1), is(empty()));
    }
    private List<Integer> factorsOf(int n) {
        return null;
    }
}

private List<Integer> factorsOf(int n) {
    return new ArrayList<>();
}

assertThat(factorsOf(2), contains(2));

private List<Integer> factorsOf(int n) {
    ArrayList<Integer> factors = new ArrayList<>();
    if (n>1)
        factors.add(2);
    return factors;
}

assertThat(factorsOf(3), contains(3));
```
```