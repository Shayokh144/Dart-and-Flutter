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