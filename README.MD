# Scala Cheat Sheet

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