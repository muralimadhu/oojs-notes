#### Private and privileged properties and methods
* In javascript, there is no explicit way to make properties private. One way to do this is using the module pattern. This uses a combination of Immediately Invoked Function Expressions (IIFE) and closures. Closures are essentially functions that can access data out of their scope.
```javascript
var person = function(){
  // private variables
  var age = 25;
  // public variables
  return {
    showAge: function(){
      return age;
    },
    growAge: function(){
      age++;
    }
  }
}();
person.showAge() // 25
person.age = 26;
person.showAge() // 25
person.growAge()
person.showAge() // 26
```
* This is great for keep members in an object private. To keep members in a custom type/constructor private
```javascript
function Person(){
      var age = 25; // private

     this.getAge = function() {
          return age;
      };

     this.growOlder = function() {
          age++;
      };
}
```
* To keep members private in a prototype
```javascript
var Person = (function() {

      // private
      var age = 25;
      function InnerPerson(name) {
          this.name = name;
      }

      InnerPerson.prototype.getAge = function() {
          return age;
      };

      InnerPerson.prototype.growOlder = function() {
          age++;
      };

      return InnerPerson; // return a different type that uses the private properties

  }());
  var person1 = new Person("Nicholas");
  var person2 = new Person("Greg");

  console.log(person1.name);      // "Nicholas"
  console.log(person1.getAge());  // 25

  console.log(person2.name);      // "Greg"
  console.log(person2.getAge());  // 25

  person1.growOlder();
  console.log(person1.getAge());  // 26
  console.log(person2.getAge());  // 26
```
* In order to create a scope-safe constructor, you can check if instance type in the constructor
```javascript
function Person(name){
  this.name = name;
}
p = Person("Heli")
console.log(p instanceof Person) // false
console.log(typeof p) // undefined
console.log(name) // Heli //global scope because new was not used
function Person(name){
  if(this instanceof Person){ // check instance type
    this.name = name
  }
  else {
    return new Person(name)
  }
}
p = Person("Heli")
console.log(p instanceof Person) // true
p = new Person("Heli")
console.log(p instanceof Person) // true
```
