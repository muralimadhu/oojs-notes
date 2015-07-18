#### Prototypes
* Constructors contain common logic that you want all your instances to have. Start with a capital letter to different them from functions
```javascript
function Person(name){
  this.name = name;
}
p = new Person("Madhu");
console.log(p.name); // Madhu
console.log(p.constructor == Person); // true
console.log(p instanceof Person); // true
```
* If you dont use the `new` keyword, Person acts like a common function where `this` points to the global object
```javascript
function Person(name){
  this.name = name;
}
p = Person("Madhu");
console.log(p instanceof Person) // false
console.log(p.name); // undefined
console.log(name); // Madhu
```
* Proptypes are like classes in languages that have classes. Its a property thats present on all objects (except for some in built functions) and is shared among all instances of an object. Any property or method present on the object that the prototype points to can be accessed by all instances of the object
```javascript
var person = {}
console.log("hasOwnProperty" in person) // true
console.log(person.hasOwnProperty("hasOwnProperty")) // false
console.log(Object.prototype.hasOwnProperty("hasOwnProperty")) // true
```
* An internal property [[Prototype]] keeps track of the prototype for an object isntance
* Use `Object.getPropertyOf` to get the prototype for an object. Essentially `a instanceof B` is true if `Object.getPrototypeOf(a) == B.prototype`. Note that .prototype can be accessed directly on the constructor, not on the instance. On the instance, Object.getPrototypeOf is used
* The prototype cannot be changed from an instance, they need to be changed from the constructor
```javascript
 var person = {}
 console.log(person.hasOwnProperty("a")) // false
 person.hasOwnProperty = function(name){
   return true;
 }
 console.log(person.hasOwnProperty("a")) // true
 Object.prototype.hasOwnProperty = function(name){
   return false;
 }
 console.log(person.hasOwnProperty("a")) // true
 delete person.hasOwnProperty;
 console.log(person.hasOwnProperty("a")) // false
 console.log(Object.getOwnPropertyDescriptor(Object.prototype, "hasOwnProperty").configurable) // true // check if hasOwnProperty can be deleted
 delete Object.prototype.hasOwnProperty
 console.log(person.hasOwnProperty("a")) // error person.hasOwnProperty is not a function
```
* The protoype can also be set like any other property
```javascript
function Person(){
}
Person.prototype = {
  toString: function(){
    console.log("My Custom toString");
  }
  constructor: Person; // make sure to set this, otherwise the .constructor property will be set to Object instead of Person
}
```
* [See Relationship between instance, constructor, prototype](https://github.com/muralimadhu/oojs-notes/tree/master/chapter4-prototypes/Prototypes.jpeg)

* Prototypes can be changed for built in types as well
```javascript
String.prototype.capitalize = function() {
    return this.charAt(0).toUpperCase() + this.substring(1);
};
"hello".capitalize() // Hello // uses autoboxing
```  
