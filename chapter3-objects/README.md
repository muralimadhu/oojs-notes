#### Objects
* Objects are dynamic, which means their properties can change at any time.

* When a property on an object is first created, an internal method [[Put]] is called. This creates memory for the property and creates an `own property` on this object. This means, the property can only be accessed through an instance of this object  

* When the value of a property changes, [[Set]] is called. 
```javascript
 var person = {}
 person.name = "John" // [[Put]]name
 person.age = "23" // [[Put]]age
 person.name = "Johnathan" // [[Set]]name
```
* To check if a property exists on an object, use the `in` operator  
Using the truthy/falsy checks on javascript can land you in trouble
```javascript
var person = {
  balance: 0,
  name: "Maddy",
  last: ""
}
console.log("balance" in person) //true
if(person.balance){console.log("Yaay")} //nothing in log // 0 is falsy
person.balance = 10
if(person.balance){console.log("Yaay")} //Yaay
if(person.last){console.log("Yaay")} //nothing in log //empty string is falsy
console.log ("last" in person) //true
console.log ("toString" in person) //true
console.log (person.hasOwnProperty("toString")) //false
```
* To delete a property, use `delete` . This calls the internal method [[Delete]]
```javascript 
delete person.balance 
```
* All objects are enumerable by default. The internal property [[Enumerable]] is set to true for many properties, but not set to true for many native methods. Use for-in to loop through properties(include properties that are set on the proptotye). Object.keys can be used to loop through properties that return true for hasOwnProperty. 
```javascript
person = {
  name: "Madhu",
  age: 21
}
person.propertyIsEnumerable("name") //true
person.propertyIsEnumerable("toString")//false
for(p in person){
  console.log(p) // name, age
  console.log(person[p]) // Madhu, 21
}
props = Object.keys(person)
for(p=0;p<props.length;p++){
  console.log(p)
  console.log(props[p])
}
```
* There are two kinds of properties. data properties (what you usually use) and accessor properties (used to get and set data). Accessor properties can be used to add additional functionality/triggers before setting/getting data. Accessor properties are enumerable
```javascript
var person = {
  _name: "Default", // _ is a convention to indicate private vars, but not mandatory
  get name(){
    console.log("getting name");
    return this._name;
  },
  set name(value){
    console.log("setting name");
    this._name = value;
  }
}
person.name = "Maddy" // setting name
console.log(person.name)// getting name, "Maddy"
```
* Object.defineProperty can be used to change attribute properties or even add new properties
```javascript
var person1 = {};
Object.defineProperty(person1, "name", {
    value: "Nicholas",
    enumerable: true, // default false
    configurable: true,// default false // only in data properties
    writable: true// default false // only in data properties
});
Object.defineProperty(person1, "age", {
  get: function(){ // only in accessor properties
    return this._age;
  },
  set: function(value){ // only in accessor properties
    this._age = value;
  },
  enumerable: false, // common to both accessor properties and data properties
  configurable: true // common to both accessor properties and data properties
});
```
* Use getOwnPropertyDescriptor to get attribute values for properties
```javascript
 var person = {name: "hello"};
 var descriptor = Object.getOwnPropertyDescriptor(person, "name")
 console.log(descriptor.enumerable) // true
```
