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
	
	  console.log("Original favourite food: " + favouriteFood);
	
	  var favouriteFood = "sushi";
	  
	  console.log("New favourite food: " + favouriteFood);
	};
	
	foodThoughts();
	```
	
	- [ ] 034. Exercise: Hoisting 3 | 1min
	- [ ] 035. Function Invocation | 7min
	- [ ] 036. arguments Keyword | 4min
	- [ ] 037. Variable Environment | 7min
	- [ ] 038. Scope Chain | 12min
	- [ ] 039. [[scope]] | 2min
	- [ ] 040. Exercise: JS is Weird | 5min
	- [ ] 041. Function Scope vs Block Scope | 4min
	- [ ] 042. Exercise: Block Scope | 4min
	- [ ] 043. Global Variables | 4min
	- [ ] 044. IIFE | 14min
	- [ ] 045. this Keyword | 17min
	- [ ] 046. Exercise: Dynamic Scope vs Lexical Scope | 12min
	- [ ] 047. call(), apply(), bind() | 11min
	- [ ] 048. Exercise: call(), apply() | 1min
	- [ ] 049. bind() and currying | 4min
	- [ ] 050. Exercise: this Keyword | 3min
	- [ ] 051. Exercise: this Keyword 2 | 1min
	- [ ] 052. Context vs Scope | 1min
	- [ ] 053. Section Review | 3min
