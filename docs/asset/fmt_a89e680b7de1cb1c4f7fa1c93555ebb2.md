
## Invoice 类

```java
items = new ArrayList<LineItem>();

billingAddress = address;
}
```

### 方法

#### 为发票添加一个产品的费用

```java
/**
 * 为发票添加一个产品的费用。
 * @param product 客户订购的产品
 * @param quantity 产品的数量
 */
public void add(Product aProduct, int quantity) {
    LineItem anItem = new LineItem(aProduct, quantity);
    items.add(anItem);
}
```

#### 格式化发票

```java
/**
 * 格式化发票。
 * @return 格式化后的发票
 */
public String format() {
    String r = "INVOICE E\n\n"
        + billingAddress.format()
        + String.format("\n%3s%-30s%8s%8s%s\n",
        "Description", "Price", "Qty", "Total:");
    for (LineItem item : items) {
        r = r + item.format() + "\n";
    }
    r += String.format("\nAMOUNT DUE: $%8.2f", getAmount());
    return r;
}
```

#### 计算应付总额

```java
/**
 * 计算应付总额。
 * @return 应付金额
 */
private double getAmount() {
    double amountDue = 0;
    for (LineItem item : items) {
        amountDue = amountDue + item.getTotalPrice();
    }
    return amountDue;
}
}
```

## section_3/LineItem.java

```java
/**
 * 描述要购买的商品数量。
 */
public class LineItem {
    private int quantity;
    private Product theProduct;

    /**
     * 根据产品和数量构造一个项目。
     * @param aProduct 产品
     * @param quantity 项目数量
     */
    public LineItem(Product aProduct, int aQuantity) {
        theProduct = aProduct;
        quantity = aQuantity;
    }

    /**
     * 计算此行项目的总成本。
     * @return 总价
     */
    public double getTotalPrice() {
        return theProduct.getPrice() * quantity;
    }

    /**
     * 格式化此项目。
     * @return 此行项目的格式化字符串
     */
    public String format() {
        return String.format("%-30s$%.2f%8d$%.2f",
            theProduct.getDescription(), theProduct.getPrice(),
            quantity, getTotalPrice());
    }
}
```

## section_3/Product.java

```java
/**
 * 描述一个具有描述和价格的产品。
 */
public class Product {
    private String description;
    private double price;

    /**
     * 根据描述和价格构造产品。
     * @param aDescription 产品描述
     * @param aPrice 产品价格
     */
    public Product(String aDescription, double aPrice) {
        description = aDescription;
        price = aPrice;
    }

    /**
     * 获取产品描述。
     * @return 描述
     */
    public String getDescription() {
        return description;
    }

    /**
     * 获取产品价格。
     * @return 价格
     */
    public double getPrice() {
        return price;
    }
}
```

## section_3/Address.java

```java
/**
 * 描述一个邮件地址。
 */
public class Address {
    private String name;
    private String street;
    private String city;
    private String state;
    private String zip;

    /**
     * 构造一个邮件地址。
     * @param name 收件人姓名
     * @param street 街道
     * @param city 市
     * @param state 州代码
     * @param zip 邮政编码
     */
    public Address(String name, String street, String city, String state, String zip) {
        name = name;
        street = street;
        city = city;
        state = state;
        zip = zip;
    }

    /**
     * 格式化地址。
     * @return 格式化的地址
     */
    public String format() {
        return name + "\n" + street + "\n" + city + "\n" + state + "\n" + zip;
    }
}
```
