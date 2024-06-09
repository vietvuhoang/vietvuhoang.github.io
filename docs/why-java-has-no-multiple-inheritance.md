# Why Java has no multiple inheritance?

Why does Java allow a class able to implement multiple **interfaces**, but allow to extend only one base class?

## What is **interface**?

First of all, interface represents the ability of some objects can do, for example 

```java
interface Flyable {
  void fly();
}

interface Poopable {
  void poop()
}

```

Something can fly, the bird can fly, the airplane can fly.
The bird can poop, the airplane cannot poop.

```java

class Bird implements Flyable, Poopable {
  ...
}

class Airplane implements Flyable {
...
}

```

But interface just describes the ability of the object, not exactly how to do it, the way birds fly by their wings is difference with airplane.


## Class characteristics 

The flyable ability doesn't not enough to define a bird, same with the pair of Flyable and Poopable ability.

```java
class Bat implements Flyable, Poopable {
  ...
} 
```

The **Bat** can fly and poop, but it is not a bird.
To be a bird, the bird will have some more attributes, the **feather** is importance one of them, the **rostrum** is another one, 
The **Bat** doesn't have both **feather**  and **rostrum**.

The classes, includes abstract classes, have their characteristics, which will not be changed through inheritance (Liskov principle).
The birds, has their characteristics, but ther Bird is a abstract class because it is require more characteristics to have a specified bird, for example the Chicken.


```java
class Chicken extends Bird {
  ...
}
```

Multiple inheritance allow the class inherits multiple characteristics from multiple source, and make the class will become complex and inconsitency with the base, the characteristics can be changed out of control, we will have a chimera which should not existing.

To simplify and keep the consistency when designing, Java doesn't allow multiple inheritance to make the class becomes high cohension.

## Exception: characteristic is changed

In nature, we will have some birds are no more flyable like Ostrich and Penguin, the characteristic is changed.

In Java, with the requirements of immutable objects, java supports __unmodifiable__ methods that will return unmodifiable collections. 
But, the immutable objects now is not cleary to marked by interface, we still accidently to call to add/remove method and get unpexpected  __UnsupportedOperationException__

For some newer language as Kotlin, the Collection is immutable by default, no more modifying methods, if you want, please implement Mutable interface to have ability of modification.





