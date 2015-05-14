#### Functions
* Functions are objects in javascript  

* Internal properties in javascript are not accessible through code. Ex) internal property for functions: [[Call]]. Internal properties define the behavior for objects. Ex) [[Call]] says, this object is executible/function  

* #### Two types of functions  
  * Function declaration
  * 
    ```javascript
     function sayHello(name){console.log(name)}
    ```
    * Can be used before its declared because function is hoisted in the context
    
  * Function expression/anonymous functions
    ```javascript
    var sayHello = function(name){console.log(name)}
    ```
    * Cannot be used before its declared, because function is not hoised in the context (either global or function scope)  
  
    ```javascript
        function foo(){
          function bar() {
              return 3;
          }
          return bar();
          function bar() {
              return 8;
          }
        }
        alert(foo()); //8 //all function declarations are hoisted on top
      ```
      ```javascript
        function foo(){
          var bar = function() {
              return 3;
          };
          return bar();
          var bar = function() {
              return 8;
          };
        }
        alert(foo()); //3 //only the var bar = undefined is hoisted. anonymous functions are not hoisted
        ```
      ```javascript
        alert(foo());
        function foo(){
          var bar = function() {
              return 3;
          };
          return bar();
          var bar = function() {
              return 8;
          };
        } //3 //only the function foo is hoisted
        ```
      ```javascript
        function foo(){
          return bar();
          var bar = function() {
              return 3;
          };
          var bar = function() {
              return 8;
          };
        }
        alert(foo()); //TypeError: bar is not a function // notice that the error is not 'bar is not defined'. bar is hoisted, but the function is not
        ```
* Functions are objects, so they can be passed along, returned, and used pretty much like any other object.
* Functions can be called with any number of arguments.The arguments object is avilable inside any function to access the arguments. The number of arguments that the function actually expects(arity) is available through function.length
  ```javascript
    function sum(input) {

      var result = 0,
          i = 0,
          len = arguments.length;

      while (i < len) {
          result += arguments[i];
          i++;
      }

      return result;
   }
    console.log(sum(1, 2));         // 3
    console.log(sum());             // 0
    console.log(sum.length) // 1
  ```
* No function overloading in javascript because there are no function signatures(functions can accept any number of arguments). 
  ```javascript
   funtion f1(a){
     console.log(a);
   }
   function f1(){
     console.log("default");
   }
   f1("hello"); //default //the last function wins
   //this is equivalent to
   var f1 = function("a","console.log(a);");
   f1 = function("console.log(\"default\")");
  ```
* When a function is attached to an object, `this` represents that object. `this` usually represents the calling object
  ```javascript
    function sayNameForAll() {
      console.log(this.name);
    }

    var person1 = {
        name: "Nicholas",
        sayName: sayNameForAll
    };

    var person2 = {
        name: "Greg",
        sayName: sayNameForAll
    };

    var name = "Michael";

    person1.sayName();      // outputs "Nicholas"
    person2.sayName();      // outputs "Greg"
    sayNameForAll();        // outputs "Michael"
  ```
  
#### Three ways to change the value of `this`
  ```javascript
       var fun = function(input){console.log(this.name + input)};
       var obj1 = {
        name: "obj1"
       }
       var obj2 = {
        name: "obj2"
       }
       console.log(fun()) //undefined
    ```
    
* call()
    `console.log(fun.call(obj1,"first"))` //obj1first

* apply()
    `console.log(fun.apply(obj1,['second']))` //obj1second

* bind() - Introduced in ECMAScript 5
    ```javascript
      first = fun.bind(obj1,"first")
      second = fun.bind(obj2, "second")
      console.log(first()) //obj1first
      console.log(second()) //obj2second
    ```
