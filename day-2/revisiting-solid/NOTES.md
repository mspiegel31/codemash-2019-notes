# Revisiting SOLID - Making the 5 principles easy enough to implement

## Overview
1. Review each solid principle
    1. definitions -  official, illustration, Tim's code
    1. Identify the benefits
    1. Identify the drawbacks

1. Tim's recommendations

## SOlID principles
1. SRP


## Single Responsibility Principle
1. Spork vs fork + spoon + knife
    1. do one thing well
    1. Tim's Definition - Every class/method should do only one logical thing.  You should be able to describe what an item does in its name.
1. code smell
    ```java
    try {
        //stuff
    } catch(Exeception e) {
        log stuff
    }
    ```
    - executing logic and logging is no good
1. Benefits
    - Better naming
    - You get to leave working code alone
    - Classes and methods become simpler
1. Drawbacks
    - you end up creating LOTS of classes and methods
    - you can't see all your logic on one screen anymore (note: who wants this?)

## Open-closed principle
1.  Tim's definition
    - Write your logic so you don't need to keep changing something that works.  Allow new features to be add on top, not inside.
1. code smell
```java
public double CalculatePay(int employeeType, double hours) {
    //insert large if block on employeeType
}
```
1. Benefits
    - code becomes more extensible
    - existing code breaks less
    - easier to distribute libraries / NuGet packages
1. Drawbacks
    - you have to anticipate what will need to change over time
        - example:  can't model gender as binary anymore...

## Liskov Substitution principle
1. Derived classes should be subsitutable by their base class
1. Tim's defintion - class inheritance should follw the "is-a" principle

1. Benefits
    - Classes behave the way they are expected to
    - Less weird bugs in your application from unimplemented methods
    - Inheritance becomes easy
1. Drawbacks
    - you can't use inheritance as a code-sharing mechanism

## Interface Segregation Principle
1. No client should be forced to implement methods it does not use.
1. Drawbacks
    - You have more interfaces
    - You have to spend more time planning out how your interfaces will be used
    - You might have to type-test an item to use other methods

## Dependency Inversion Principle
1. Tim's defintion: interfaces alll the way down.  Dependencies should be sent  _down_ the chain, rather than having the bottom units _request_ their dependencies
    - _Dependency Injection_ is a solution to the principle of _Dependency Inversion_.
1. Benefits:
    - easy replacement/upgrade of components
    - testable
1. Drawbacks
    - Interfaces Everywhere!
    - Not as simple as `new`ing things in place.

## Tim's Top 3 Tasks
1. Move your dependencies out using interfaces and injection
1. Slim down your methods, especially the really big ones or the ones that have duplication
    - you'll probably wind up with a couple methods that only call 20 other methods
1. Create smaller, composable interfaces