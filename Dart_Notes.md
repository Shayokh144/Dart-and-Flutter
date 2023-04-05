# Dart

- main()
	- The special, required, top-level function where app execution starts
- var
	- A way to declare a variable without specifying its type.
- Dart uses the keywords `const` and `final` for values that don’t change.
- final
	- `final` acts like `val` in Kotlin or `let in Swift`
- Use `const` for values that are known at compile-time. Use `final` for values that don’t have to be known at compile-time but cannot be reassigned after being initialized.
- Everything you can place in a variable is an object, and every object is an instance of a class. Even numbers, functions, and null are objects. With the exception of null (if you enable sound null safety), all objects inherit from the Object class.
- If you enable null safety, variables can’t contain null unless you say they can. You can make a variable nullable by putting a question mark (?) at the end of its type. For example, a variable of type int? might be an integer, or it might be null. If you know that an expression never evaluates to null but Dart disagrees, you can add ! to assert that it isn’t null (and to throw an exception if it is). An example: `int x = nullableButNotNullInt!`
- Unlike Java, Dart doesn’t have the keywords public, protected, and private. If an identifier starts with an underscore (_), it’s private to its library.
- You don’t have to initialize a local variable where it’s declared, but you do need to assign it a value before it’s used.
- `late` modifier, which has two use cases:
	- Declaring a non-nullable variable that’s initialized after its declaration.
	- Lazily initializing a variable.
	- Eample: `late String description;`

## Class

- Class example:

```Dart
class Spacecraft {
  String name;
  DateTime? launchDate;

  // Read-only non-final property
  int? get launchYear => launchDate?.year;

  // Constructor, with syntactic sugar for assignment to members.
  Spacecraft(this.name, this.launchDate) {
    // Initialization code goes here.
  }

  // Named constructor that forwards to the default one.
  Spacecraft.unlaunched(String name) : this(name, null);

  // Method.
  void describe() {
    print('Spacecraft: $name');
    // Type promotion doesn't work on getters.
    var launchDate = this.launchDate;
    if (launchDate != null) {
      int years = DateTime.now().difference(launchDate).inDays ~/ 365;
      print('Launched: $launchYear ($years years ago)');
    } else {
      print('Unlaunched');
    }
  }
}
```
- Object creation example:

```Dart
var voyager = Spacecraft('Voyager I', DateTime(1977, 9, 5));
voyager.describe();

var voyager3 = Spacecraft.unlaunched('Voyager III');
voyager3.describe();
```
- [Constructor in details](https://dart.dev/language/constructors)

## Inheritance

- Dart has single inheritance.

```Dart
class Orbiter extends Spacecraft {
  double altitude;

  Orbiter(super.name, DateTime super.launchDate, this.altitude);
}
```
## Mixins

- Mixins are a way of reusing code in multiple class hierarchies. The following is a mixin declaration:

```Dart
mixin Piloted {
  int astronauts = 1;

  void describeCrew() {
    print('Number of astronauts: $astronauts');
  }
}
```
- To add a mixin’s capabilities to a class, just extend the class with the mixin.

```Dart
class PilotedCraft extends Spacecraft with Piloted {
  // ···
}
// PilotedCraft now has the astronauts field as well as the describeCrew() method.
```

## Interfaces and abstract classes

- Dart has no interface keyword. Instead, all classes implicitly define an interface. Therefore, you can implement any class.

```Dart
class MockSpaceship implements Spacecraft {
  // ···
}
```

## Important concepts

- Everything you can place in a variable is an object, and every object is an instance of a class. Even numbers, functions, and null are objects. With the exception of null (if you enable sound null safety), all objects inherit from the Object class.


- Although Dart is strongly typed, type annotations are optional because Dart can infer types. In the code above, number is inferred to be of type int.

- If you enable null safety, variables can’t contain null unless you say they can. You can make a variable nullable by putting a question mark (?) at the end of its type. For example, a variable of type int? might be an integer, or it might be null. If you know that an expression never evaluates to null but Dart disagrees, you can add ! to assert that it isn’t null (and to throw an exception if it is). An example: `int x = nullableButNotNullInt!`

- When you want to explicitly say that any type is allowed, use the type Object? (if you’ve enabled null safety), Object, or—if you must defer type checking until runtime—the special type dynamic.

- Dart supports generic types, like `List<int>` (a list of integers) or `List<Object>` (a list of objects of any type).

- Dart supports top-level functions (such as main()), as well as functions tied to a class or object (static and instance methods, respectively). You can also create functions within functions (nested or local functions).

- Similarly, Dart supports top-level variables, as well as variables tied to a class or object (static and instance variables). Instance variables are sometimes known as fields or properties.

- Unlike Java, Dart doesn’t have the keywords public, protected, and private. If an identifier starts with an underscore (_), it’s private to its library.

- Identifiers can start with a letter or underscore (_), followed by any combination of those characters plus digits.

- Dart has both expressions (which have runtime values) and statements (which don’t). For example, the conditional expression condition ? expr1 : expr2 has a value of expr1 or expr2. Compare that to an if-else statement, which has no value. A statement often contains one or more expressions, but an expression can’t directly contain a statement.

- Dart tools can report two kinds of problems: warnings and errors. Warnings are just indications that your code might not work, but they don’t prevent your program from executing. Errors can be either compile-time or run-time. A compile-time error prevents the code from executing at all; a run-time error results in an exception being raised while the code executes.





































