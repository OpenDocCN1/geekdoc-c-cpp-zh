# The Basic CSS Selectors

CSS works by defining the styles of the elements on a Web page using CSS rules. Rules are applied using selectors, which come in three basic varieties: HTML selectors are used to reference a specific tag; class selectors, which are applied individually to elements; or an ID selector that is applied to a single element on the page (Table 3.1). You will use these three basic selectors constantly, and they are the best place to start. In Chapter 4, you will learn about using other selectors for creating more selective styling.

TABLE 3.1 Basic Selectors What Elements Are Styled Compatibility

| Format | Selector Name | What Elements Are Styled | Compatibility |
| --- | --- | --- | --- |
| a | HTML | All specified HTML tags | IE4, FF1, S1, C1, O3.5, CSS1 |
| .myClass | Class | Any HTML tag where class is applied | IE4, FF1, S1, C1, O3.5, CSS1 |
| a.myClass | Dependent Class | Specified HTML tag where class is applied | IE4, FF1, S1, C1, O3.5, CSS1 |
| #myID | ID | Any HTML tag where ID is applied | IE4, FF1, S1, C1, O3.5, CSS1 |
| a#myID | Dependent ID | Specified HTML tag where ID is applied | IE4, FF1, S1, C1, O3.5, CSS1 |
| * | Universal | All HTML tags | IE7, FF1, S1, C1, O3.5, CSS2 |