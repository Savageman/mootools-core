Type: Function {#Function}
==========================

Function Methods.

### See Also:

- [MDC Function][]



Function: Function.from {#Function:Function-from}
----------------------------------------

If the passed argument is a function, it will return itself. Otherwise, it will return a function that returns the passed argument.

### Syntax:

	var foo = Function.from(obj);
	
### Arguments:

1. obj - (*mixed*) If this argument is a function, it will simply return itself. Otherwise, an object you wish to convert into a function that returns the argument.

### Returns:

* (*function*) Either the passed function or an anonymous function that returns the passed argument.

### Examples:

	var fn = Function.from(42);
	alert(fn());	// alerts '42'
	
	var fn2 = Function.from(fn);
	alert(fn2());	// alerts '42'
	
### Notes:

This function is equivalent to the following deprecated MooTools 1.2 methods:

	var fn1 = Function.from();		// Equivalent to var fn1 = $empty();
	var fn2 = Function.from(foo);	// Equivalent to var fn2 = $lambda(foo);


Function: Function.attempt {#Function:Function-attempt}
-----------------------------

Tries to execute a number of functions. Returns immediately the return value of the first non-failed function without executing successive functions, or null.

### Syntax:

	Function.attempt(fn[, fn, fn, fn, ...]);

### Arguments:

* fn   - (*function*) The function to execute.

### Returns:

* (*mixed*) Standard return of the called function.
* (*null*) `null` if all the passed functions fail.

### Examples:

	var result = Function.attempt(function(){
		return some.made.up.object;
	}, function(){
		return jibberish.that.doesnt.exists;
	}, function(){
		return false;
	});

	//result is false

	var failure, success;

	Function.attempt(function(){
		some.made.up.object = 'something';
		success = true;
	}, function(){
		failure = true;
	});

	if (success) alert('yey!');

### Notes:

This method is an equivalent of *$try* from MooTools 1.2.



Function method: extend {#Function:extend}
---------------------------------

Add methods to a function

### Syntax:

	myFunction.extend(key,value);

### Arguments:

1. key - (*string*) The key of the prototype
2. value - (*mixed*) The function or another value of the protoype

### Example: 

	var myFunction = function(){};
	myFunction.extend('alert',function(text){
		alert(text);
	});
	myFunction.alert('Hello!'); // Alerts Hello!


Function method: implement {#Function:implement}
---------------------------------------

Add methods to the prototype

### Syntax:

	myFunction.implement(key,value);

### Arguments:

1. key - (*string*) The key of the prototype
2. value - (*mixed*) The function or another value of the protoype

### Example: 

	var myFunction = function(){};
	myFunction.implement('alert',function(text){
		alert(text);
	});
	var myInstance = new myFunction();
	myInstance.alert('Hello!'); // Alerts Hello!

### Notes:

The difference between *implement* and *extend*, is that implement adds the value to the prototype.
So with *implement* each instance of the function will have this method or property while with *extend*
the method or property is added to a single instance.


Function method: attempt {#Function:attempt}
---------------------------

Tries to execute a single function. Returns immediately the return value of the function if it does not fail, or null.

### Syntax:

	var myFunctionResult = myFunction.attempt(args[, bind]);

### Arguments:

1. args - (*mixed*) An argument, or array of arguments to run the function with.
2. bind - (*object*, optional) The object that the "this" of the function will refer to.

### Returns:

* (*mixed*) This Function's return value.
* (*null*) `null` if the function fails.

### Examples:

	var myFunction = function(){
		return some.made.up.object;
	};
	myFunction.attempt(); // Returns: 'null'


	var myFunction = function(val){
		return val;
	};
	myFunction.attempt(false); // Returns: 'false'

### See Also:

- See [Function.attempt](#Function:Function-attempt) for using more than one functions.



Function method: run {#Function:run}
---------------------------

Runs the Function with specified arguments and binding. The same as apply but reversed and with support for a single argument.

### Syntax:

	var myFunctionResult = myFunction.run(args[, bind]);

### Arguments:

1. args - (*mixed*) An argument, or array of arguments to run the function with.
2. bind - (*object*, optional) The object that the "this" of the function will refer to.

### Returns:

* (*mixed*) This Function's return value.

### Examples:

#### Simple Run:

	var myFn = function(a, b, c){
		return a + b + c;
	}
	var myArgs = [1,2,3];
	myFn.run(myArgs); //Returns: 6


#### Run With Binding:

	var myFn = function(a, b, c) {
		return a + b + c + this;
	}
	var myArgs = [1,2,3];
	myFn.run(myArgs, 6); //Returns: 12



Function method: pass {#Function:pass}
-----------------------------

Returns a closure with arguments and bind.

### Syntax:

	var newFunction = myFunction.pass([args[, bind]]);

### Arguments:

1. args - (*mixed*, optional) The arguments to pass to the function (must be an array if passing more than one argument).
2. bind - (*object*, optional) The object that the "this" of the function will refer to.

### Returns:

* (*function*) The function whose arguments are passed when called.

### Example:

	var myFunction = function(){
		var result = 'Passed: ';
		for (var i = 0, l = arguments.length; i < l; i++){
			result += (arguments[i] + ' ');
		}
		return result;
	}
	var myHello = myFunction.pass('hello');
	var myItems = myFunction.pass(['peach', 'apple', 'orange']);

	//Later in the code, the functions can be executed:
	alert(myHello()); //Passes "hello" to myFunction.
	alert(myItems()); //Passes the array of items to myFunction.



Function method: bind {#Function:bind}
-----------------------------

Changes the scope of `this` within the target function to refer to the bind parameter.

### Syntax:

	myFunction.bind([bind[, args]]);

### Arguments:

1. bind - (*object*, optional) The object that the "this" of the function will refer to.
2. args - (*mixed*, optional) The arguments to pass to the function (must be an array if passing more than one argument).

### Returns:

* (*function*) The bound function.

### Example:

	function myFunction(){
		//Note that 'this' here refers to window, not an element.
		//The function must be bound to the element we want to manipulate.
		this.setStyle('color', 'red');
	};
	var myBoundFunction = myFunction.bind(myElement);
	myBoundFunction(); //This will make myElement's text red.


Function method: delay {#Function:delay}
-------------------------------

Delays the execution of a function by a specified duration.

### Syntax:

	var timeoutID = myFunction.delay(delay[, bind[, args]]);

### Arguments:

1. delay - (*number*) The duration to wait (in milliseconds).
2. bind	 - (*object*, optional) The object that the "this" of the function will refer to.
3. args	 - (*mixed*, optional) The arguments passed (must be an array if the arguments are greater than one).

### Returns:

* (*number*) The JavaScript timeout id (for clearing delays).

### Example:

	var myFunction = function(){ alert('moo! Element id is: ' + this.id); };
	// Wait 50 milliseconds, then call myFunction and bind myElement to it.
	myFunction.delay(50, myElement); //Alerts: 'moo! Element id is: ... '

	// An anonymous function which waits a second and then alerts.
	(function(){ alert('one second later...'); }).delay(1000);
	
	// To stop the delay, clearTimeout can be used like so
	var timer = myFunction.delay(50);
	clearTimeout(timer);


### See Also:

- [MDC setTimeout][], [MDC clearTimeout][]



Function method: periodical {#Function:periodical}
-----------------------------------------

Executes a function in the specified intervals of time. Periodic execution can be stopped using the [$clear][] function.

### Syntax:

	var intervalID = myFunction.periodical(period[, bind[, args]]);

### Arguments:

1. period - (*number*) The duration of the intervals between executions.
2. bind	  - (*object*, optional) The object that the "this" of the function will refer to.
3. args	  - (*mixed*, optional) The arguments passed (must be an array if the arguments are greater than one).

### Returns:

* (*number*) The Interval id (for clearing a periodical).

### Example:

	var Site = { counter: 0 };
	var addCount = function(){ this.counter++; };
	addCount.periodical(1000, Site); //Will add the number of seconds at the Site.
	
	// The interval can be stopped using the clearInterval function
	var timer = myFunction.periodical(1000);
	clearInterval(timer);

### See Also:

- [MDC setInterval][], [MDC clearInterval][]


Deprecated Functions {#Deprecated-Functions}
============================================

Function method: create {#Deprecated-Functions:create}
------------------------------------------------------

This function has been deprecated.

Function method: bindWithEvent {#Deprecated-Function:bindWithEvent}
------------------------------------------------------------------

This function has been deprecated.

### Example how you could replace this method:

	myElement.addEvent('click',function(e){
		myFunction.bind(bind, [e]);
	});


[options]: #Function:create:options
[Element:addEvent]: /core/Element/Element.Event/#Element:addEvent
[MDC Function]: https://developer.mozilla.org/en/Core_JavaScript_1.5_Reference/Global_Objects/Function
[MDC setInterval]: https://developer.mozilla.org/en/DOM/window.setInterval
[MDC setTimeout]: https://developer.mozilla.org/en/DOM/window.setTimeout
[MDC clearInterval]: https://developer.mozilla.org/en/DOM/window.clearInterval
[MDC clearTimeout]: https://developer.mozilla.org/en/DOM/window.clearTimeout
[Function:delay]: /core/Types/Function/#delay
[Function:periodical]: /core/Types/Function/#periodical

