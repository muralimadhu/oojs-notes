#### Inheritance
* Javascript's inheritance is called prototypal inheritance. Since properties on the protoype can be accessed by all object instances, inheritance is achieved. All objects by default inherit from Object.prototype
```javascript
var book = {name: "Sapiens"};
console.log(Object.getPrototypeOf(book) === Object.prototype) // true
console.log(book.constructor); // function Object(){}
```
* Methods available on `Object.prototype`
 * `hasOwnProperty` -> Check if a property belongs to an object
 * `valueOf` -> Used when an operation is performed on an object (comparison for example)
 * `toString` -> String representation of the object, also used as a fallback if `valueOf` returns a reference
 * `isPrototypeOf` -> Check if an object is the prototype of another object
 * `propertyIsEnumerable` -> Check if a property is enumerable (shows up in `Object.keys` and when for looping over the object)

* Object.prototype can be modified, but this can have devastating consequences, so beware. 
```javascript
Object.prototype.toString = function(){
  console.log("Dont do this!!");
}
person = {name: "Hello"}; 
person.toString(); // Dont do this
```
* The simplest form of inheritance is Object Inheritance. When creating the object, specify the prototype ([[Prototype]] property). This is by default set to `Object.prototype`
```javascript
 var person = Object.create(Object.prototype, {name: {value: "Madhu"}, sayName: {}});
 // is equivalent to saying
 var person = {name: "Madhu", sayName: function(){console.log(this.name)}};
 var person1 = Object.create(person, {name: {value: "Dee"}});
 console.log(person.sayName()) // Madhu
 console.log(person1.sayName()) // Dee
 console.log(person.isPrototypeOf(person1)) // true
 console.log(person1.hasOwnProperty("name")) // true
 console.log(person1.hasOwnProperty("sayName")) // false
```
* You can also create objects with a null prototype, but they are generally not very useful
```javascript
 var person = Object.create(null);
 console.log(person.hasOwnProperty) // undefined
```
* Every function has a `prototype` property. Every object has a `[[prototype]]` internal property that points to the prototype. Every object also has a `constructor` that points to the constructor used to create the object. By default, for all objects, the constructor is `function Object(){}`, the `[[prototype]]` property points to `Object.prototype` and `Object.prototype.constructor` also points to `function Object(){}`. The prototype chain ends at `Object.prototype` as `Object.getPrototypeOf(Object.prototype)` points to `null` 
```javascript
function Person(){
  
}
// internally the javascript engine does this
Person.prototype = Object.create(Object.prototype, {
  constructor: {
    configurable: true,
    enumerable: true,
    value: Person,
    writable: true
  }
})
```
```javascript
function Rectangle(length, width) {
      this.length = length;
      this.width = width;
  }
console.log(Object.getPrototypeOf(Rectangle.prototype) == Object.prototype) // true
console.log(Rectangle.prototype.constructor == Rectangle) // true
Rectangle.prototype.getArea = function() {
      return this.length * this.width;
  };
console.log(Rectangle.prototype.hasOwnProperty("getArea")) // true
console.log(Rectangle.prototype.hasOwnProperty("toString")) // false
Rectangle.prototype.toString = function() {
    return "[Rectangle " + this.length + "x" + this.width + "]";
};
console.log(Rectangle.prototype.hasOwnProperty("toString")) // true
function Square(size) {
      this.length = size;
      this.width = size;
}
Square.prototype = new Rectangle();
console.log(Object.getPrototypeOf(Square.prototype) == Rectangle.prototype) // true
console.log(Square.prototype.constructor) // undefined (we just overwrote this)
Square.prototype.constructor = Square;
s = new Square(5); 
console.log(s.toString()) //"[Rectangle 5x5]"
Square.prototype.toString = function() {
      return "[Square " + this.length + "x" + this.width + "]";
  };
console.log(s.toString()) //"[Square 5x5]"
```
* The Rectangle constructor is not really doing anything special. So instead of calling the constructor, `Object.create` can be used to link Square to `Rectangle.prototype`
```javascript
function Rectangle(length, width) {
      this.length = length;
      this.width = width;
  }
function Square(size){
  this.length = size;
  this.width = size;
}
Square.prototype = Object.create(Rectangle.prototype, {
  constructor: {
    value: Square,
    enumerable: true,
    configurable: true,
    writable: true
  }
});
```
*  [See Relationship between Square and Rectangle](https://github.com/muralimadhu/oojs-notes/tree/master/chapter5-inheritance/Inheritance.jpeg)
