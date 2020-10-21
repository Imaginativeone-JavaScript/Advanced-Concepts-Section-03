- [ ] Section 3: Javascript Foundation II 0/26 | 2hr 31min
	- [x] 028. Section Overview | 1min
	  - [ ] Execution Context
	  - [ ] Lexical Environment
	  - [ ] Scope Chain
	  - [ ] Hoisting
	  - [ ] Function Invocation
	  - [ ] Function Scope vs Block Scope
	  - [ ] Dynamic vs Lexical Scope
	  - [ ] this, call, apply, bind
	  - [ ] IIFE
	- [x] 029. Execution Context | 9min
	  - How do we run code in JavaScript?
	    - Assign Variables
	    - Run Functions
	    - As soon as a pair of parentheses is encountered >> Execution Context
	      - The context is placed onto the Call Stack
	    - Consider: "The Global Execution Context"
	      - global()
	        - Popped off the stack after our final line of code is run
		- Global Object
		- this
		- Take a look at an empty file
		- this and window are there this === window (Node: "Global")
		- Creation Phase
		  - HOISTING
		- Execution Phase (Run my code)
	- [ ] 030. Lexical Environment | 6min
	  - "Where you write something"
	  - "Little Universes that get created every time we create an Execution Context"
	  - Lexical analysis >> "What universe is it part of?"
	    - Where did we write the function?
	  - **At Compile Time** Where was the code written?
	- [ ] 031. Hoisting | 11min
	  - The behavior of moving variables and function-declarations to the top(s) of their respective environments
	  
	  **Condition 1**
	  
	  ```javascript
	  console.log('1------');
	  console.log(teddy);
	  console.log(sing());
	  
	  var teddy = 'bear';
	  
	  function sing() {
	    console.log('ohhh la la la');
	  }
	  ```

	  **Condition 2**
	  
	  ```javascript
	  console.log('1------');
	  
	  // Upon 'var' or 'function' >> "Reserve memory for this entity in Memory Heap; not moved up"
	  var teddy = undefined; // teddy PARTIALLY hoisted here; JS engine during the creation phase
	  			 // 'const' or 'let' doesn't get hoisted; 'teddy' is not defined

	  function sing() {	 // function (declaration) FULLY hoisted here assigned a location in memory
	  			 // Putting this function in parentheses gives me a reference error,
				 // as 'function' not encountered
	    console.log('ohhh la la la');
	  }
	  
	  var sing2 = function() { 	// function EXPRESSION; sing2 gets hoisted and equals undefined
	  				// sing2() must follow its call to be defined
	    console.log('uhhh la la la');
	  }

	  console.log(teddy);
	  console.log(sing());
	  
	  var teddy = 'bear';
	  ```

	- [ ] 032. Exercise: Hoisting | 4min
	
	```javascript
	one = undefined; // DURING HOISTING, 'one' = 'undefined'; 2nd line is ignored
	
	var one = 1;
	var one = 2;
	
	console.log(one); // 'one' yields the number 2
	```
	
	```javascript
	a(); 	// DURING HOISTING, 2nd function replaces the first IN THE MEMORY LOCATION, producing 'bye'
		// no matter where a() is called
	
	function a() {
	  console.log('hi');
	}
	
	function a() {
	  console.log('bye');
	}
	```
	
	- [ ] 033. Exercise: Hoisting 2 | 7min
	
	```javascript
	var favouritefood = "grapes";
	
	var foodThoughts = function() {
	
	  console.log("Original favourite food: " + favouriteFood); 	// CREATION PHASE: var favouriteFood is assigned 'undefined'
	  								// CREATION PHASE: var foodThoughts is assigned 'undefined'
	  								// CREATION PHASE: var favouriteFood = 'grapes' is ignored
	  var favouriteFood = "sushi";					// EXECUTION PHASE: favouriteFood = 'grapes' (var keyword is removed)
	  								// EXECUTION PHASE: foodThoughts = function()
									
									THEN
									
									// A new Execution Context is created, with its associated
	  console.log("New favourite food: " + favouriteFood);		// HOISTING CREATION PHASE
	};
	
	foodThoughts();
	```
	
	- I can try to avoid hoisting by not using var and using const or let instead
	
	- [ ] 035. Function Invocation | 7min
	
	  - Programs are simply 'assigning variables to memory' and then running functions with the variables.
	
	```javascript
	// Function Expression
	var canada = () => { 	// Defined at RUN TIME
	  console.log('cold');
	}
	
	// Function Declaration
	function india() {	// Defined at PARSE TIME, when the compiler looks at the code and starts allocating memory and hoisting
	  console.log('warm');
	}
	
	// Function Invocation/Call/Execution
	canada();	// Create an Execution Context
	india(); 	// Create an Execution Context
	```
	
	  - When a function is invoked, we create a new Execution Context on top of our Global Execution Context
	  - Also, we get the 'this' keyword
	  - unlike the global context, we also get 'arguments'
	  - See the marry() function below:
	  
	```javascript
	// Function Expression
	var canada = () => { 	// Defined at RUN TIME
	  console.log('cold');
	}
	
	// Function Declaration
	function india() {	// Defined at PARSE TIME, when the compiler looks at the code and starts allocating memory and hoisting
	  console.log('warm');
	}
	
	// Function Invocation/Call/Execution
	canada();	// Create an Execution Context // cold
	india(); 	// Create an Execution Context // warm
	
	function marry(person1, person2) {
	  console.log('arguments', arguments);			// arguments {0: 'Tim', 1: 'Tina' }
	  return `${person1} is now married to ${person2}`;	// => 'Tim is now married to Tina'
	}
	
	marry('Tim', 'Tina');
	```
	
	- [ ] 036. arguments Keyword | 4min
	  - arguments is not an array
	  - It is iterable, however
	  
	  ```javascript
	  console.log(Array.from(arguments)); // ['Tim', 'Tina']
	  ```
	  ```javascript 
	  function marry2(...args) { // Spread Operator
	    console.log('arguments', args);			// arguments {0: 'Tim', 1: 'Tina' }
	    console.log(Array.from(arguments)); 			// ['Tim', 'Tina']

	    return `${args[0]} is now married to ${args[1]}`;	// => 'Tim is now married to Tina'
	  }
	  ```
	  
	  ```javascript
	  india();
	  console.log(arguments); // {} Empty 'arguments' object
	  ```
	  
	- [ ] 037. Variable Environment | 7min
	
	  - Variables need to know how they relate to one another
	  
	  ```javascript
	  function two() {	// CREATION PHASE: Hoisted
	    var isValid;	// Undefined
	  }
	  
	  function one() {	// CREATION PHASE: Hoisted
	    var isValid = true;	// EXECUTION PHASE: local variable environment
	    two();		// New Execution Context
	  }
	  
	  var isValid = false; 	// CREATION PHASE: Hoisted; isValid = undefined
	  			// EXECUTION PHASE: Assigned false
	  
	  one();		// EXECUTION PHASE: Execution Context Created
	  
	  // Call stack, Execution Contexts ----------------------------------
	  // two() // placed into the stack after one()	// isValid = undefined
	  // one() // placed into the stack first	// isValid = true
	  // global() 					// isValid = false
	  ```
	
	- [ ] 038. Scope Chain | 12min
	
	  ```javascript
	  function findName() {
	    var b = 'b';
	    return printName();
	  }
	
	  function printName() {
	    var c = 'c';
	    return 'Andre Neagoie';
	  }
	
	  function sayMyName() {
	    var a = 'a';
	    return findName();
	  }
	
	  sayMyName();
	  ```
	  - Each context has a link to its outside-world/parent
	  - All of these functions have access to the global scope
	  - Scope chain gives us access to the Parent Environment
	  - "Static Scope", Lexical Scope
	  
	  ```javascript
	  function sayMyName() {
	    var a = 'a';
	    return function findName() {
	      var b = 'b';
	      // console.log(c);
	      return function printName() {
	        var c = 'c';
		return 'Andre Neagoie';
	      }
	    }
	  }
	  
	  sayMyName(); 		// [Function: findName]
	  sayMyName()();	// [Function: printName]
	  sayMyName()()();	// 'Andre Neagoie'
	  ```
	  
	- [ ] 039. [[scope]] | 2min
	- [ ] 040. Exercise: JS is Weird | 5min
	
	  ```javascript
	  function weird() {
	    height = 50;	// Not declared, "Leakage of global variables"
	    return height;
	  }
	  ```
	  
	  'use strict' was added to get rid of the weirdness
	  
	  ```javascript
	  var heyhey = function doodle() {
	    // do something
	    return 'heyhey';
	  }
	  
	  heyhey(); // 'heyhey'
	  doodle(); // Reference Error, can only access it in heyhey
	  ```
	  
	- [ ] 041. Function Scope vs Block Scope | 4min
	
	```javascript
	if (5>4) {
	  var secret = '12345';
	}
	
	secret(); // '12345'
	
	With const/let, block scope, can't get the secret
	```
	
	- [ ] 042. Exercise: Block Scope | 4min
	
	```javascript
	function loop() {
	  for (var i=0; i<5; i++) {
	    console.log(i);		// 1 through 4
	  }
	  console.log('final', i); 	// 5
	}
	
	loop();
	
	What happens with let? Inaccessible
	```
	
	- [ ] 043. Global Variables | 4min
	  - Global variables are "evil"?
	  - Polluting the global namespace
	  - Limited Memory, makes the Browser slow/crash
	  - Garbage Collection
	  - Variable Collision/Overwrites
	
	- [ ] 044. IIFE | 14min
	  - Immediately Invoked Function Expression
	  
	  ```javascript
	  ( // Function Expression
	    function() { // Anonymous Function
	  
	    }
	  )();
	  
	  // New execution context with a new variable environment
	  ```
	  
	  ```javascript
	  var script1 = (function() {
	    function a() {
	      return 5;
	    }
	    return { a: a }
	  })(); // Remember to immediately invoke the function
	  
	  script1.a() // 5
	  ```
	  
	- [ ] 045. this Keyword | 17min
	
	  - **this** is the object that the **function** is a property of 
	
	- [ ] 046. Exercise: Dynamic Scope vs Lexical Scope | 12min
	- [ ] 047. call(), apply(), bind() | 11min

	- [ ] 048. Exercise: call(), apply() | 1min
	- [ ] 049. bind() and currying | 4min
	- [ ] 050. Exercise: this Keyword | 3min
	- [ ] 051. Exercise: this Keyword 2 | 1min
	- [ ] 052. Context vs Scope | 1min
	- [ ] 053. Section Review | 3min
