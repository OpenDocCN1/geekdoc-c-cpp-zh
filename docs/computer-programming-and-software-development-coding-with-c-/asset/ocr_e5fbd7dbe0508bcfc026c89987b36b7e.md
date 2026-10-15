```
export interface IProduct {
    productId: number;
    productName: string;
    productCode: string;
    releaseDate: Date;
    price: number;
    description: string;
    starRating: number;
    imageUrl: string;
}
```

We define an interface using the interface keyword followed by the interface name, which is often the name of the thing that the interface describes. By some naming conventions, the interface is prefixed with an i for interface, though many TypeScript developers leave off this prefix. The export keyword here at the front exports this interface, thereby making it available for use anywhere in the application. The body of the interface defines the set of properties appropriate for this type. This example defines the properties for a product. For each property, the interface includes the property name, a colon, and the property data type. Once we have defined an interface, we can use it as a data type. We import the interface and then use the interface name as the data type, just like we used other data types such as string or boolean. We are back in the sample application looking at the ProductListComponent. Here we see that we defined our products array as any. So let's create an interface that defines what a product is. We'll put the interface into its own file in