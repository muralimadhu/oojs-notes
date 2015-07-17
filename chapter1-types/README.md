#### Types

* Two types in javascript - **primitive types** and **reference types** 

* ##### Primitive types: string, number, boolean, null, undefined
  ```javascript
  //number
  var num1 = 12;
  var num2 = 12.5;
  //string
  var str = "hello";
  //boolean
  var bool = true;
  //null
  var something = null; //only value 
  //undefined
  var something = undefined;//only value
  var anotherThing; //automatically assigned undefined 
  ```

  * value copied into variables
  
  ```javascript
  var m1 = "hello";
  var m2 = m1;
  m1 = "world";
  console.log(m1); //world
  console.log(m2); //hello
  ```
  * can use `typeof` operator to find primitive types
  * methods available for string, number, boolean just like objects. This is done using autoboxing. A temporary object is created and then destroyed so methods are available on primitive types just like reference types
  ```javascript
  var m1 = "hello";
  console.log(m1.slice(1)); //ello
  m1.test = "test";
  console.log(m1.test); //undefined
  //internally
  var m1 = "hello";
  var temp = new String(m1);
  console.log(temp.slice(1)); //ello
  temp = null;
  temp = new String(m1);
  temp.test = "test";
  temp = null;
  temp = new String(m1);
  console.log(temp.test);//undefined
  ```


* ##### Reference types: Array, Function, Object, Error, Regexp, Date
  * variables contain memory location of object instance
  ```javascript
  var obj1 = new Object();
  var obj2 = obj1;
  obj1.prop = "hello";
  console.log(obj2.prop); //hello
  ```
  * Literal representations for each type instead of using new
  ```javascript
  var objLit = {};
  var funLit = function(){console.log(1)};
  var arryLit = [1, 2, 3];
  var numbers = /\d+/g;
  ```
  * Use instanceof operator to find reference types
  ```javascript
  var items = [];
  var object = {};
  function reflect(value) {
      return value;
  }
  console.log(items instanceof Array);        // true
  console.log(items instanceof Object);       // true
  console.log(object instanceof Object);      // true
  console.log(object instanceof Array);       // false
  console.log(reflect instanceof Function);   // true
  console.log(typeof reflect) //function
  console.log(reflect instanceof Object);     // true
  ```


* ##### Gotchas
  * Using literals instead of  `new` calls the same code but doesnt call the `new Object()` constructor

  * ```javascript 
      var x = null;
      console.log(typeof x); //object
      console.log(x === null); //true
      console.log(x == undefined)//true
      console.log(x === undefined)//false
    ``` 
