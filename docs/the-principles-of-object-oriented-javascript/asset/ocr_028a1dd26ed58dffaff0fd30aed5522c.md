```
Rectangle.prototype.getArea = function() {
    return this.length * this.width;
};

Rectangle.prototype.toString = function() {
    return "[Rectangle " + this.length + "x" + this.width + "]";
};

// inherits from Rectangle
function Square(size) {
    Rectangle.call(this, size, size);
    // optional: add new properties or override existing ones here
}

Square.prototype = Object.create(Rectangle.prototype, {
    constructor: {
        configurable: true,
        enumerable: true,
        value: Square,
        writable: true
    }
});

Square.prototype.toString = function() {
    return "[Square " + this.length + "x" + this.width + "]";
};

var square = new Square(6);

console.log(square.length);      // 6
console.log(square.width);        // 6
console.log(square.getArea());    // 36
```

The ① Square constructor calls the Rectangle constructor and passes in this as well as size two times (once for length and once for width). Doing so creates the length and width properties on the new object and makes each equal to size. This is the way to avoid redefining properties from a constructor from which you want to inherit. You can add new properties or override existing ones after applying the super type constructor.

This two-step process is useful when you need to accomplish inheritance between custom types. You'll always need to modify a constructor's prototype, and you may also need to call the supertype constructor from within the subtype constructor. Generally, you'll modify the prototype for method inheritance and use constructor stealing for properties. This approach is typically referred to as pseudoclassical inheritance because it mimics classical inheritance from class-based languages.