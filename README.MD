# Scala/Java/C\# Cheat Sheet

Using scala/java cheat sheet from [this](http://techblog.realestate.com.au/java-to-scala-cheatsheet/) article by Ken Scambler. Adding C# equivalents.

## Annotation Declarations

### Scala
```scala
trait Foo extends StaticAnnotation {
}
```

### Java
```java
@interface Foo {
}
```

### C\#  
```csharp
class Foo : System.Attribute {
       
}
```
- There is no special syntax for annotation definitions.
- An annotation has to extend scala.Annotation, or one of its sub-traits.
- Scala’s compiler will stitch it into the necessary bytecode form for use in Scala or Java.
 
## Annotation Use

### Scala
```scala
@Foo
class Blah {
    @Stuff
    def doStuff(): Unit = ()
}
```
### Java
```java
@Foo
public class Blah {
    @Stuff
    public void doStuff() {}
}
```
### C\#  
```csharp  
[Foo]
public class Blah {
    [Stuff]
    public void doStuff() {}
}
```
- Same annotation usage syntax.
- Annotations are not used very often in Scala.
- The extra power of lambdas, types and implicits means that the extra-linguistic meta-programming that they are required for in Java often doesn’t need to happen.
- Annotations can nest, like in Java.

## Array Access

### Scala
```scala
numbers(0)
```
### Java
```java
numbers[0]
```
### C\#  
```csharp
numbers[0]
```
- There is no special syntax for arrays.
- Anything defining an apply() method can use function-like syntax like this.

## Array Assignment

### Scala
```scala
numbers(0) = 5
```
### Java
```java
numbers[0] = 5
```
### C\#  
```csharp
numbers[0] = 5
```
- There is no special syntax for arrays.
- Anything defining an update() method can use assignment syntax like this.

## Array Creation

### Scala
```scala
val strs = Array("a", "b")
```
### Java
```java
String[] strs = new String[] {"a", "b"}
```
### C\#  
```csharp
string[] strs = {"a", "b"}
```
- Arrays don’t have privileged syntax; they look the same as other generic collections.
- Only use them if you need co-location in memory for high performance.
- Instead of using “new”, we are calling the factory function on the Array object.
- Abstracts over the different kinds of JVM array representations int[], Object[], long[], etc, using black magic.

## Autoboxing

### Scala
```scala
val a: AnyRef = 4 //box
val b: Int = a.asInstanceOf[Int] // unbox
```
### Java
```java
Integer a = 4; // box
int b = a; // unbox
```
### C\#  
```csharp
Int32 a = 4; // box
int b = a; // unbox
```
- Autoboxing and unboxing happens automatically and invisibly.
- See Primitives.

## Builder

### Scala
```scala
class Point(val x: Int = 3, val y = 77)
// x = 5, y = 77
new Point(x = 5)
```
### Java
```java
public class Point {
    private final int x, y;
    
    static class Builder {
        int x = 0;
        int y = 0;
        
        public void withX(int x) {
            this.x = x;
        }
        
        public void withY(int y) {
            this.y = y
        }
        public Point build() {...}
    }   
    
    public int getX() {
        return x;
    }
    
    public int getY() {
        return y;
    }
    // and on and on with more fields
}
```
### C\#  
```csharp
public class Point
{
    public int X { get; }
    public int Y { get; }

    static class Builder
    {
        static int x, y = 0;

        public static void withX(int xIn) {
            x = xIn;
        }

        public static void withY(int yIn) {
            y = yIn;
        }

        public static Point Build() {...}
        }
    }
}
```
- Scala has named and default parameters.
- You can use this with regular constructors and factory methods, no need for builders.

## Casts

### Scala
```scala
myFruit.asInstanceOf[Banana]
```
### Java
```java
(Banana)myFruit
```
### C\#  
```csharp
(Banana)myFruit
```
- Casting doesn’t have a special syntax, it is a method.
- The syntax is deliberately verbose, to discourage casting.
- Casts are not very idiomatic Scala; mostly the type system should protect you from having to lie to it.

## Class Declaration

### Scala
```scala
class Gumble
```
### Java
```java
public class Gumble {}
```
### C\#  
```csharp
public class Gumble {}
```
- Everything is public by default.
- Don’t need braces if there’s no content.

## Class implementing interfaces/mixins

### Scala
```scala
class Shoe extends Shineable
    with Cobbleable with Wearable
```
### Java
```java
public class Shoe implements
    Shineable, Cobbleable, Wearable {}
```
### C\#  
```csharp
public class Shoe : Shineable, Cobbleable, Wearable {}
```
- The first thing always says “extends”, even if it is a trait.
- “with” for everything else.
- This determines the order in which trait mixins are applied.

## Class with constructor, binding to instance variables with accessors

### Scala
```scala
class Point(val x: Int, val y: Int)
```
### Java
```java
public class Point {
    private final int x, y;
    
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
    
    public int x() {
        return x;
    }
    
    public int y() {
        return y;
    }
}
```
### C\#  
```csharp
public class Point {
    public readonly int x;
    public readonly int y;
    
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```
- Adding “val” makes the constructor arg bind to a field of the same name.
- “Instance variables” are actually hidden; what you call is always an accessor method, that can be overridden.

## Class with constructor, superclass

### Scala
```scala
class Gumble(id: String) extends Foo(id)
```
### Java
```java
public class Gumble extends Foo {
    public Gumble(String id) {
        super(id)
    }
}
```
### C\#  
```csharp
public class Gumble : Foo 
{
    public Gumble(String id) : base(id) {}
}
```
- Primary constructor goes in the declaration.
- Type comes after the identifier.

## Enums

### Scala
```scala
// Algebraic Data Type (ADT)
sealed trait Suit
case object Spades extends Suit
case object Hearts extends Suit
case object Clubs extends Suit
case object Diamonds extends Suit
val suit: Suit = Spades

// or

// Enumeration class
object Suit2 extends Enumeration {
    val Spades, Hearts, Clubs, Diamonds = Value
}

val suit2: Suit2.Value = Suit2.Spades
```
### Java
```java
enum Suit {SPADES, HEARTS, CLUBS, DIAMONDS}
Suit suit = Suit.SPADES;
```
### C\#  
```csharp
enum Suit { SPADES, HEARTS, CLUBS, DIAMONDS }
Suit suit = Suit.SPADES;
```
- Scala doesn’t directly support enums; one of the few things in Java that can’t be generated from Scala. People constantly complain about this, but you really don’t need them.
- There are two techniques commonly used; Algebraic Data Types, which are more general and powerful, and the Enumeration mixin, which is less powerful.
- ADTs are a closed hierarchy of ordinary classes and objects; here we are using top-level objects, because we require no parameters.
- “case class” and “case object” is syntax sugar that generates fields, hashcode, equals, toString and factory methods. They are ordinary classes/objects that you could otherwise have defined by hand. Here, “case object” just gives us a toString() the same as the identifier name.
- The Enumeration mixin defines a type Value; the Value method creates a new value of type Value.
- Notice that unlike most languages, comma-separated declarations get assigned to every variable in the list, not just the last one.
- Usually you would prefer ADTs; the Enumeration mixin is quite limited in usage.

## Equality (value)

### Scala
```scala
any1 == any2
```
### Java
```java
obj1.equals(obj2);
primitive1 == primitive2;
```
### C\#  
```csharp
obj1.Equals(obj2);
primitive1 == primitive2;
```
- == is a method that everything supports.
- It calls the equals() method on objects.
- It checks value equality on primitives.
- It is null-safe.
 
 ## Equality (reference)
 
 ### Scala
 ```scala
 obj1 eq obj2
 ```
 ### Java
 ```java
 obj1 == obj2;
 ```
 ### C\#  
 ```csharp
 obj1 == obj2;
 ```
- eq is a method that all objects (any class under AnyRef) support.
- Reference equality is not usually used in functional programming.
- If the reference provides object identity, then it implies that the state of the object mutates over time.
- In FP, identity is usually modelled outside of object instances.

## Factory

### Scala
```scala
() => Foo
```
### Java
```java
public interface FooFactory {
    public Foo createFoo()
}
```
### C\#  
```csharp
public interface FooFactory {
    public Foo createFoo()
}
```

## For Loop

### Scala
```scala
// Low level equivalent
var i = 0
while (i < max) {
    doStuff(i)
    i += 1
}

// Index counting equivalent
for (i <- 0 until max) {
    doStuff(i)
}

// Obtain index alongside item with combinators
for ((item, i) <- myList.zipWithIndex) {
    doStuff(item, i)
}
```
### Java
```java
for (int i=0; i < max; i++)
{
    doStuff(i);
}
```
### C\#  
```csharp
for (int i = 0; i < max; i++)
{
    doStuff(i);
}
```
- There’s no direct equivalent to the low-level for loop; you would need to use while.
- No one has used this in Java since 1999 anyway.
- You can use a for-comprehension if you just want run through a range.
- start.to(includedEnd).by(step) and start.until(excludedEnd).by(step) are the most common methods used to create range objects.
- The “to” and “until” methods are supported on all numeric types.
- The range is a collection, although it doesn’t explicitly store all of the numbers in range, of course.
- At the cost of an extra iteration, the most concise way to obtain the index alongside elements in a sequence is zipWithIndex.
- “0 until max” is the same as “0.until(max)”. Any instance method can be written in operator style.
