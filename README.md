Objective-C Coding Style
================================

Table of Contents
-----------------

1.  [Spacing and Formatting](#spacing-and-formatting)
2.  [Brackets](#brackets)
3.  [Naming](#naming)
4.  [Comments](#comments)
5.  [Pragma Marks](#pragma-marks)
6.  [Constants](#constants)
7.  [Return Early](#return-early)
8.  [Initializers](#initializers)
9.  [Headers](#headers)
10. [Nullability](#nullability)
11. [Strings](#strings)
12. [Dot Notation](#dot-notation)

Spacing and Formatting
-----------------------------

### Whitespace
* Use **TAB** indentation and alignment. Do not use spaces.
* Trailing whitespace is acceptable only on blank lines, but discouraged even there.
  * In Xcode, select "Automatically trim whitespace" and "Including whitespace-only lines" in Text Editing preferences
    to handle this automatically.
* Put spaces after commas, and before and after operators.
* Do not put spaces between parentheses and what they are enclosing.

**Example:**
```objc
foo("bar")
```

**Not:**

```objc
foo( "bar" )
```

### Containers
* Array one-liners are acceptable unless they have too many items or their values are too long.

```objc
NSArray *array = @[@"uno", @"dos", @"tres", @"cuatro"];
```

* In that case, break them in several lines:

```objc
NSArray *array = @[
    @"This is how we do, yeah, chilling, laid back",
    @"Straight stuntin’ yeah we do it like that",
    @"This is how we do, do do do do, this is how we do",
];
```

* Dictionary one-liners are reserved for single pairs only:

```objc
NSDictionary *dict = @{@"key" : @"highway"};
```

* Format it pretty otherwise, leaving a trailing comma after the last item:
```objc
NSDictionary *dict = @{
    @"key1" : @"highway",
    @"key2" : @"heart",
};
```

Brackets
--------
* Always use brackets for `if` / `for` / `while` / `do`-`while` statements. Even if its a one-liner:
* Always use line break before opening brackets
  * ... and after the closing bracket if followed by more statements

```objc
if (itsMagic)
{
  [self makeItEverlasting];
}
```

* Write follow up `else` clauses after the previous closing bracket on the same line.

```objc
if (hasClue)
{
  knowExactlyWhatToDo();
}
else if (seeItAllSoClear)
{
  writeItDown();
}
else
{
  sing();
  dance();
}
```

Naming
------
* Follow Apple’s [Coding Guidelines for Cocoa](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)
on naming.

Comments
--------
* Use the `//` style for single line comments or when appending comments in the same line of code.
* Use the `/* */` style for multi-line comments.

**Example:**
```objc
/*
 * This is a multi-line comment. The opening and closing markers are on their
 * own lines, and each other line is preceded by a * that is indented by one
 * space.
 *
 * This is a new paragraph in the same block comment.
 */

stop(); // Hammer-time!

// this is a very brief comment.
```

Pragma Marks
------------
* Use the pre-processor instruction `#pragma mark` to mark related groups of methods.
* Use 2 empty line before and 1 after the `#pragma mark`

```objc
-(void)someMethod
{
  // ...
}


#pragma - New Method groups

-(void)methodNextOne
{
  // ...
}
```

Constants
---------
* Do not define constants using `#define`.
* Publicly (or privately) exposed variables should be constant (trying to assign values will result in compilation
error).

```objc
extern NSString const *MYCodeStandardErrorDomain;
```

Return Early
------------
* Return early on errors and failed pre-conditions to avoid unnecessary nested brackets and / or unnecessary
computations.

**Example:**

```objc
-(void)setFireToTheRain:(id)rain
{
  if ([_rain isEqualTo:rain])
  {
    return;
  }

  _rain = rain;
}
```

Initializers
------------
* Follow [Apple's typical init format](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/EncapsulatingData/EncapsulatingData.html#//apple_ref/doc/uid/TP40011210-CH5-SW11) to initialize objects.

**Example:**

```objc
-(instancetype)init
{
  self = [super init];

  if (self)
  {
    // initialize instance variables here
  }

  return self;
}
```

Headers
-------
* The use of prefix headers has been deprecated. Do not add new code to an existing prefix header.
* When importing a module use the hash-import variant instead of at-import.
  * Yes: `#import <Foundation/Foundation.h>`
  * No: `@import Foundation;`

Nullability
-----------
* Use `NS_ASSUME_NONNULL_BEGIN` and `NS_ASSUME_NONNULL_END` in header files, and explicitly add `nullable` when needed. Example:

```objc
#import <Foundation/Foundation.h>

@protocol MYProtocol;

NS_ASSUME_NONNULL_BEGIN

typedef void(^MYSomeBlock)(NSData * _Nullable data, NSError  _Nullable *error);

@interface MYTYourClass : NSObject

@property (nonatomic, copy, readonly, nullable) NSString *customString;
@property (nonatomic, strong, readonly) id<MYProtocol> protocol;

-(nullable instancetype)initWithProtocol:(id<MYProtocol>)protocol
                            customString:(nullable NSString *) customString;

@end

NS_ASSUME_NONNULL_END
```

Strings
-------
* All strings presented to the user should be localized.

Dot Notation
------------
* Use bracket notation when calling non-accessor methods:

```objc
[self doSomething];
```

* Use bracket notation when accessing globals through a class method:

```objc
[MyClass sharedInstance];
```

* Use dot notation where you could:

```objc
[MyClass.sharedInstance doSomething];
```

* Set and access properties using dot notation:

```objc
self.myString = @"A string";
```
