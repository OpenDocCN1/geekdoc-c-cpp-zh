```
    public class SortTest {
        @Test
        public void nothing() throws Exception {

        }
    }
```

```
    public class SortTest {

        @Test
        public void sorted() throws Exception {
            assertEquals(asList(), sort(asList()));
        }
        private List<Integer> sort(List<Integer> list) {
            return null;
        }
    }
```

```
    private List<Integer> sort(List<Integer> list) {
        return new ArrayList<>();
    }
```

```
    assertEquals(asList(1), sort(asList(1)));
```

```
    private List<Integer> sort(List<Integer> list) {
        return list;
    }
```

```
    assertEquals(asList(1, 2), sort(asList(1, 2)));
```

```
    assertEquals(asList(1, 2), sort(asList(2, 1)));
```