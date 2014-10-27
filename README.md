#Creating methods

##The four elements

A method can be described by its five parts:

1) The method name
2) Its type (instance or class)
3) Its arguments (aka parameters)
4) Its return type
5) And its associated implementation

Let's take an example to get acquainted with methods.

######Example
```objc

- (void)addIntegerNumber:(NSNumber *)integerNumberToAdd {
	
	//some code goes here to implement the addition of an integer with another number.

}

```

###Method name

Here we are looking at a method named `addIntegerNumber:`. We traditionally refer to the name of the method without it's arguments (that which comes after the colons) or its return types. In fact, you'll often see the name of the method referred to in code as the selector. Or in this case, to be more specific `@selector(addIntegerNumber:)`.

Note that nothing is abbreviated in this method name. In Objective-C you will come across very long method names, unlike other languages. XCode's autocomplete feature comes in very handy as a result. Starting typing the name of a method and you'll see it quickly rise to the top of the list of autocomplete options.

###Method type

The above method is an instance method. This is designated by the `-` in front of the method name.

To refresh on the difference between a class / instance method, check our reading: [Intro To Objects](https://github.com/flatiron-school-curriculum/reading-ios-introToObjects#difference-between-an-instance-and-a-class).

Clearly, the above method should be an instance method, as we would not want to add a specific integer number to the entire class, but rather to a specific instance of an `NSNumber`.

###Arguments

We can pass information to a method via its arguments. We designate a method has an argument with the `:`, followed by the argument's type in parentheses, and then a name for our argument. We can then refer to this argument in our code block by this name.

######Example
```objc

- (void)addIntegerNumber:(NSNumber *)integerNumberToAdd {
	
	NSInteger convertedNumberToInteger = [integerNumberToAdd integerValue];

	// more code to make this method work
	...

}
```

Methods may also have multiple arguments.

######Example
```objc

- (void)operation:(NSString *)operationType WithNumber:(NSNumber *) {
	
	//Write some code to take any operation (e.g. addition, subtraction, multiplication, etc.) and do that with an NSNumber
}
```

In this case our selector (aka method name) would be `operation:WithNumber:`.

###Return type

In all of the examples presented so far, our methods have begun with a `-` and then the word `void` in parentheses. This is where we indicate the return type of our method. Do we want the result of our method to be passed back to the point at which we called the method? If so, we must include a return type. If not, we can use `void`.

Additionally if we want to return a result, we must make sure to declare `return` (and the variable / value we want to return) within our method. Don't forget that the returned variable / value must be of the type specified by the return type in our method name! (In our example, that would be an `NSNumber`.)

######Example
```objc
-(NSNumber *)addIntegerNumber:(NSNumber *)integerNumberToAdd {
	
	NSNumber *computedResult;

	//some code goes here to implement the addition of an integer with another number using computedResult

	return computedResult;
}
```

###Associated implementation

The fact that a method has an associated implementation is rather self-evident, but to be complete, we must ensure that a method has some associated code block that defines what it does. In all of our above examples, we have left most of the code block to your imagination.


###Nested method calls

Methods may be, and often are, nested like so.

```objc

[[self.ourNumber addIntegerNumber:@5] addIntegerNumber:@10];

```

##Method invocation

We give a short intro to method invocation (aka "calling a method", aka "sending a message") [here](https://github.com/flatiron-school-curriculum/reading-ios-introToObjects#difference-between-an-instance-and-a-class).

