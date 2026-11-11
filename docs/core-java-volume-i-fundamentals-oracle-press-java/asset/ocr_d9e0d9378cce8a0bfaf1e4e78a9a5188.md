```
~~~java
76      */
77      public <T> void forType(TypeLiteral<T> type, Function<T, String> formatterForType)
78      {
79          rules.put(type, formatterForType);
80      }
81
82      /**
83       * Formats all fields of an object using the rules of this formatter.
84       * @param obj an object
85       * @return a string with all field names and formatted values
86       */
87      public String formatFields(Object obj)
88              throws IllegalArgumentException, IllegalAccessException
89      {
90          var result = new StringBuilder();
91          for (Field f : obj.getClass().getDeclaredFields())
92          {
93              result.append(f.getName());
94              result.append("=");
95              f.setAccessible(true);
96              Function<?, String> formatterForType = rules.get(TypeLiteral.of(f.getGenericType()));
97              if (formatterForType != null)
98              {
99                  // formatterForType has parameter type ?. Nothing can be passed to its apply
100                 // method. Cast makes the parameter type to Object so we can invoke it.
101                 @SuppressWarnings("unchecked")
102                 Function<Object, String> objectFormatter
103                         = (Function<Object, String>) formatterForType;
104                 result.append(objectFormatter.apply(f.get(obj)));
105             }
106             else
107                 result.append(f.get(obj).toString());
~~~
```