#Breaking Down Methods

Methods in Objective-C may look a little intimidating at first, but all methods can be broken down into five parts:

1. **Name**
2. Type: **instance** or **class**
3. **Arguments** (aka parameters)
4. **`return`** type 
5. Associated Implementation ("**what does it actually do?**")

Let's use an example to get acquainted with methods.

######Example
```objc
- (void) stripVowelsFromString: (NSString *) stringWithVowels {
	
	/* some code goes here to use 
	the string that's passed in (stringWithVowels)
		and remove its vowels. */
}
```
##Method Name
Our method's named `stripVowelsFromString:`. This is what you'd call it in a conversation, as well as *how* you'd call it in code. The `:` denotes that it *takes an argument*. We'll get into arguments later, but for now just know that a colon is part of the name and signifies that it needs some input to work.

####Naming Conventions
Note that nothing is abbreviated in this method name. In Objective-C you will come across and create very long method names. For example, you've been using `didFinishLaunchingWithOptions:` and thats a mouthful!

Your method names should be descriptive, but *try* to be succinct. I say *try* because it's okay for them to be long — make them as long as you need them to be to get the point across! But also make sure they make sense to you, and really convey what the point is. If you **name your methods to have clear intentions**, your code will be more readable for future you and others. 

####Auto-Complete
You may ask, "but won't writing long method names steer us toward a typo-ridden hell?". **Fear not, XCode's got auto-complete.** Thanks to auto-complete, writing long methods is a *breeze*. Just starting typing the name of a method and you'll see it quickly rise to the top of the list of autocomplete options. Use the up/down arrows to scroll through the list once it appears.

*Top-Tip: is the method you're looking for not showing up in auto-complete? Make sure you've started with a* `[` *and that you're in the correct scope.*

##Method Type (Instance vs. Class)

Every method definition begins with either a `-` (*instance*) or a `+` (*class*). Our example method is an instance method, because it starts with a `-`. To make our example a class method, it's as simple as replacing the `-` with a  `+` in it's definition.

####Instance Methods

Since our example is an instance method, it can only be **called on an instance of its class**. Imagine we wrote this in a custom class called `FISStringFormatter`. This is an instance method, so to call it we'd need to have an actual object ("*an instance of `FISStringFormatter`*") in the first place! 

####Class Methods

Conversely, a class method is **called on the Class itself**. When calling one, the class is the sender. As it turns out, you've been using a class method when you create an instance of a class! `[NSArray alloc]` look familiar? That calls the method `alloc` on the `NSArray` class.

*For more on the difference between class / instance methods, check our reading: [Intro To Objects](https://github.com/learn-co-curriculum/reading-ios-introToObjects#difference-between-an-instance-and-a-class).*

##Arguments

We can pass information to a method via its arguments. To define a method argument, add a `:` followed by the argument's type in parentheses, and then a name for our argument. We can then refer to this argument in our code block by this name.

######Example
```objc
- (void) logStringWithMuchEnthusiasm: (NSString *) stringToLog {
	
	// our argument is called 'stringToLog'
	// in the definition, we just use it like a normal variable
	NSLog(@"HEY! %@ !!!", stringToLog);
}
```
When this gets called, `stringToLog` becomes whatever you pass into  the method. In the definition, the **argument is simply a placeholder**, allowing you to specify what's done with information a user passes in. 

So if you called `[exampleObject logStringWithMuchEnthusiasm: @"I love iOS"]`, this method would simply replace `stringToLog` with your inputted string and log `"HEY! I love iOS !!!"`. 

####Multiple Arguments
Methods may also have multiple arguments. In Objective-C, that means adding more to the name *after* an argument. Let's create a method which takes both a string and an integer. It looks like this: 

######Example
```objc

- (void) logString: (NSString *)stringToLog withInteger: (NSInteger)integerToLog {
	// code that logs both arguments in some interesting way
}
```
So this method's name is `logString:withInteger:`. From the name you can tell there are two arguments because there are two `:`. 

In it's definition, notice how we have the `:` and specify our first argument's type and name. Then, the method name continues on (`withInteger:`), specifying that theres another argument. There is no limit on how many arguments a method may have, *but don't shove too much into a single method!*.

##Return Type

In the examples, our methods have begun with `- (void)`. We know what the `-` is for (method type), but what's up with that second part? This is where we specify our method's return type. **Return type is how a method indicates what its output is**. 

So we can put any type necessary in that first parenthesis, and it would mean our method *must* output that type in order to run. If it doesn't, you'll raise a compiler error and your program will not build. 

#####`(void)`

You'll see and use this frequently in method definitions. `void` is from C and means "nothing" (not to be confused with `nil`; void is a *type*, while nil is a *value*). So if you make `void` your method's return type, that means "this method doesn't return anything". This also means you don't need a `return` statement in your method. Use this whenever you feel that a method doesn't need any output. 

##### How Do I `return`?

If you specify a return type (any type that isn't `void`), you must make sure to end your method with `return _______;`, where the blank is data of whatever type you specified. Again, the variable / value must be of the type specified as the return type in our method name! Otherwise your code will not be able to run.

######Example
```objc
-(NSString *) pluralizeString:(NSString *) stringToPluralize {
	
	// we'll just add 's' for example's sake
	NSString *outputString = [NSString stringWithFormat: @"%@s", stringToPluralize]; 

	return outputString;
}
```
##### How Do I Use a Returned Value?
If a method returns a value, that means a value is the result of the method call (`[objectName methodName]`). So we can use a method call just like any other statement that has a value (such as `2 + 2` or `@"Hello"`). Let's use `pluralizeString` again:

````objc
NSString *myPluralizedString = [exampleObject pluralizeString: @"cat"];
// ^ now myPluralizedString is @"cats"
````
Basically we can put the call wherever we would need its returned value. Try and **visualize your method call to represent the value you expect it to return**. Don't worry if this doesn't click right away, it will make sense with more practice.

##Associated Implementation (The Fifth Element!)

*Obviously* a method needs code inside that does the darn thing, but we couldn't just ignore the fact.

Most of the examples leave implementation up to your imagination, but a method could be as simple as 2 lines — above all else, methods are here for **convenience**. They exist so we don't have to implement the same stuff over and over again in our program! Here's a few tips for good method implementation:

   * **A method should do one thing and do it well**. "One thing" is almost always up for interpretation, but try and make your methods as simple as possible.
   * **Implement methods clearly** — use however many lines, comments or variables you need so that someone who's never seen it before can understand whats going on under the hood. Take care of future you.
   * **If you find yourself doing the same process** over and over again (three times or more~), you should probably just write a method.

*Remember that these are tips, not rules!*

##Method Invocation
If you need a refresher on method invocation (aka "calling a method", or "sending a message"), check out our reading: [Using Methods](https://github.com/learn-co-curriculum/reading-ios-using-methods).

