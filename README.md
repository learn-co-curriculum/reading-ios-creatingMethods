# Writing Methods

## Objectives

1. Review the steps to calling methods.
2. Know the syntax for declaring methods.
3. Recognize when to declare methods as either private or public and how to do so in Objective-C.
4. Be able to write a method body.
5. Know where to place `return` in the method body.

## Review: Calling A Method

In the earlier reading about calling methods, we discussed the four elements of making a method call:

```objc
ReturnType *captureVariable = [recipientObject methodNameArgument:argumentVariable];
```
From left to right these are:

1. The variable of the correct type used to capture the return,
2. The name of the object to perform the method,
3. The name of the method being called, and
4. The names of any objects submitted to the methods as arguments. 

**Note:** *Remember, not all methods supply a return or require arguments.*

As you should recall, a **method** is a behavior that an **object** can perform upon itself. Methods are the action sequences of our code. The ability to write custom methods is one of the primary elements of structured programming that makes it a flexible tool for solving a wide variety of problems. Fundamentally, methods allow us to run the exact same section of code multiple times from pretty much anywhere within our application that we wish.

The real beauty of methods lies in not needing to understand all of the ins-and-outs of how any single method works in order to apply that method to given circumstance. Sure, we need to understand *what* the method does in order to apply it appropriately, but that's a far cry from knowing its inner workings. A helpful image is of using a common applicance like a vending machine: you don't need a degree in mechanical engineering in order to trade a handful of coins for a soda—you simply need to meet the input requirements ($1.25 in change) and understand its interface (press a button).

But how exactly does the vending machine accept the payment, receive the instruction, and return the correct result? Well, that's the job of the designer to figure out!

## Method Anatomy 201

Before we dive into writing a method from scratch, let's reference an existing method to get acquainted with the practice. While there are four elements to a method call, there is a fifth element to composing a new one (and no—it isn't Milla Jovovich). All together, they are:

1. **Instance or Class Indicator:** respectively the `-` or `+` at the beginning of the line,
2. **Return Type:** the class within the `(``)` ("parentheses") which is the kind of instance variable that the method will result to,
3. **Method Name:** a description of what the method does, which may contain:
4. (optional) **Arguments:** instance variables to be passed into the method which are relevant to its operation, and
5. **Method Body:** the set of instructions that calling the method executes.

As an example of a method definition, let's look at the `AppDelegate`'s `application:didFinishLaunchingWithOptions:` method:

```objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Override point for customization after application launch.

    return YES;
}
```
**Note:** *You'll notice that Apple's methods are written in camel case. This is considered standard practice and you should follow it. Notice also that the continuation of the method name following the first argument* `application:` *resumes in camel case beginning with a* ***lowercase*** *letter,* `didFinishLaunchingWithOptions:`. *Resuming a method declaration in capital case is regarded as bad style and should be avoided.* 

Let's review each element of this method:

1. The `-` ("dash") immediately tells us that this is an instance method and not a class method. (We'll cover class methods in a later topic on inheritance.) For the time being, any methods that we direct you to write will be instance methods, but the `-` symbol is an important signal to the compiler that you're beginning a method declaration or definition, so don't forget it.

2. We also know pretty quickly that this method returns a `BOOL` value, the purpose of which we can infer from the method name that it is meant to represent whether or not the method has been called and completed.

3. Method names sometimes take a little deciphering. Herein lies the value of descriptive and appropriate naming styles. We can infer from this name that, in the life cycle of the `AppDelegate` instance, this method is called implicitly *after* the application has launched. The past tense verb "did" is an indicator of the `BOOL` return value (it is phrased as answer a yes or no question). And, the argument descriptors are appropriate to the expected input objects.

4. The arguments, you'll notice, are in two elements: a type and a name. The argument type tells us what class of variable is expected, and the argument name tells us what will be the internal name of the variable passed into the argument when the method is called. In the above case, two arguments are expected: a `UIApplication` object internally named `application`, and an `NSDictionary` of options internally named `launchOptions` (the use of the plural is a clue that this is a collection). 

5. The method body contained inside the curly braces (`{``}`), which contains the instructions for how the method should go about doing what its meant to do. Since this method says it returns a `BOOL` value, we need to end the method with a `return` statement with a `BOOL`—in this case, a `YES`.

That's how we can read a method definition that's already been built. Now we're going to walk through the steps of creating our own method from scratch.

## Declaring A Method

Every Objective-C class exists in two separate files, the "**header**" file with the extention `*.h` and the "**implementation**" file with the extension `*.m`. The first step in writing a custom method is to **declare** the method in the header file and then **define** it in the implementation file.

**Advanced:** *Methods don't actually need to be declared in the header file in order to work. Doing so makes them accessible to other classes and enables Xcode's autocomplete function to work. Autocomplete is an important tool for both avoiding bugs caused by typos and for double-checking that the compiler is correctly aware of whatever thing you're typing.*

Method declarations are placed between the `@interface` and `@end` markers of the header and contain only the first four elements of the method—that is everything except the body—and end with a semicolon (`;`) like a property declaration.

#### Example:

In the header file for our example class `FISVendingMachine`, let's declare an instance method that's going to accept a selection (an integer) and a payment amount (also an integer) as arguments and then return a soda (in the form of a string). Let's be sure to give it a descriptive name:

```objc
@interface FISVendingMachine : NSObject

- (NSString *)deliverSodaForSelection:(NSUInteger)selection withPaymentInCents:(NSUInteger)paymentInCents;

@end
```
**Note:** *Usage of the* `*` *("star") symbol in method declarations and definitions follows the same convention as declaring variables of that type anywhere in the code. Above, the* `NSString` *return type uses a* `*` *because it is an object variable, while the two* `NSUInteger` *arguments do not because they are primitive variables.*

Great! Now lets switch to the implementation file and define the method.

## Defining A Method

Declaring a method is just giving it a name. To actually write out the instructions that it's meant to represent, however, is the heart of the problem and is what gives the method life.

In the implementation file, similar to the `@interface` and `@end` markers in the header file, the method definition must be placed between the `@implementation` and the `@end`. If you've declared the method name in the header file, autocomplete should offer it up once you start typing its name. If it doesn't, then this may be an indicator that your method hasn't been correctly declared.

Instead of ending the statement with a `;`, however, we're going to follow the method name with a pair of curly braces `{``}` which will enclose the instructions that we want the method to perform.

**Tip-tip:** *Keep close track of your closing curly braces* `}`. *If you unconsciously begin defining a new method before properly closing the previous method, the compiler will get very confused and generate a slew of errors, possibly even saying that it can't find the* `@end` *marker for the file. Mind those curly braces!*

#### Example: `FISVendingMachine`

Defining our custom method on our `FISVendingMachine` class will begin like this:

```objc
@implementation

- (NSString *)deliverSodaForSelection:(NSUInteger)selection withPaymentInCents:(NSUInteger)paymentInCents {
	return nil;
}

@end
```
**Note:** *When writing a method with a return type, it is acceptable to start with just a* `return nil;` *return statement in order to silence the compiler error while you work on the method. Just be careful that you don't forget to change this to return your found result.*

Let's get into it by first defining some internal variables for the sodas in stock (as an array of strings) and the cost of a soda (as an integer). Let's also set the `return` statement to pass back a default string so that it isn't returning `nil`:

```objc
- (NSString *)deliverSodaForSelection:(NSUInteger)selection withPaymentInCents:(NSUInteger)paymentInCents {

    NSArray *stock = @[ @"Swizzle Soda",
                        @"Mr. Fizz",
                        @"Buzz Doctor",
                        @"De Bug Beer",
                        @"Moth Machine!",
                        @"Liquid Ice"     ];
    
    NSUInteger costInCents = 125;

	return @"Test Soda";
}
```
Great! Now we have our inventory and our cost set up for us to utilize.

Let's figure out how to access the stock and return the correct soda for the selection. Our interface designer has told us that the vending machine has buttons "1" through "6". Most humans prefer to count from one—not zero like computers (and programmers). We'll have to handle this discrepancy in our method body, otherwise we'll produce one kind of what's called an "off by one" error.

Knowing this, we can simply access the `stock` array by using `selection` minus one to index it. We can capture the return from this into a string variable named `soda`. Let's write this out: 

```objc
- (NSString *)deliverSodaForSelection:(NSUInteger)selection withPaymentInCents:(NSUInteger)paymentInCents {

    NSArray *stock = @[ @"Swizzle Soda",
                        @"Mr. Fizz",
                        @"Buzz Doctor",
                        @"De Bug Beer",
                        @"Moth Machine!",
                        @"Liquid Ice"     ];
    
    NSUInteger costInCents = 125;

    NSString *soda = stock[selection - 1];
    
    return @"Test Soda";
}
```
Now that we've accessed the correct soda, we can return that instead of our test string:

```objc
...
    return soda;
}
```
Our method will now return the customer's desired soda. Good job! We're not done just yet, though. We still need to incorporate a check that the customer paid the correct amount.

### Multiple `return` Statements

The `return` statement passes back the final result of the method. A method body can actually contain any number of `return` statements. However, any code following the first `return` statement that executes *will not get run* during that call because the method has already concluded itself. This is relevant because a method can have multiple patterns of resolution based upon context. It's especially useful for checking that the submitted arguments are valid inputs.

Let's use a second, albeit earlier, return statement to tell the customer if they haven't supplied enough payment. If we nest this second return statement inside of an `if` statement, it will only run if the check fails (or in terms of the `BOOL`, if it's positive for an error).

```objc
- (NSString *)deliverSodaForSelection:(NSUInteger)selection withPaymentInCents:(NSUInteger)paymentInCents {
    
    NSArray *stock = @[ @"Swizzle Soda",
                        @"Mr. Fizz",
                        @"Buzz Doctor",
                        @"De Bug Beer",
                        @"Moth Machine!",
                        @"Liquid Ice"     ];
    
    NSUInteger costInCents = 125;
    
    if (paymentInCents < costInCents) {
        return @"Insufficient payment."
    }
    
    NSString *soda = stock[selection - 1];
    
    return soda;
}
```
Now if our method is called and supplied a payment amount below `125`, a soda won't be returned, but rather an "error" message will read out.

**Advanced:** *The* `NSError` *class is designed specifically for passing error messages around. This is significantly more advanced than the current topic so we're just using* `NSString` *to keep the example simple.*

## Calling Your Custom Method

Now that we've finished writing our custom method, we can call it elsewhere in our code just like any other method (so long as our custom class `FISVendingMachine` has been properly imported):

```objc
FISVendingMachine *vendOMatic = [[FISVendingMachine alloc] init];
    
NSString *soda = [vendOMatic deliverSodaForSelection:1 
                                  withPaymentInCents:125];
    
NSLog(@"%@", soda);
```
This will print: `Swizzle Soda`.

Now anyone with access to a `FISVendingMachine` object can call our `deliverSodaForSelection:withPaymentInCents:` method and get a soda without knowing how our custom method works internally.

 Mmmm... swizzlin'.



<p data-visibility='hidden'>View <a href='https://learn.co/lessons/reading-ios-creatingMethods' title='Writing Methods'>Writing Methods</a> on Learn.co and start learning to code for free.</p>
