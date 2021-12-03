# Dart warmup

Type-safe general purpose programming language designed for building fast apps on multiple platforms.

Was supposed to be an alternative to Javascript but was not really embrassed by the Web development community. It bounced back and was adopted by the Flutter framework.

It's unique in its ability to compile to multiple targets:
- ARM64 machine code for mobile devices
- Javascript for Web Browsers
- Self contained executables (i.e. x86_64) for Widnows, MacOs, Linux

Has a JIT compiler which compiles source code to machine code on the fly, which can boost developer productivity with features like hot-reload in Flutter.

All Dart code runs inside of an `isolate` which is a chunk of memory running in a single threaded event-loop, which makes it possible to perform asynchronous background work on a single thread. Dart also allows us to spaw multiple isolates to run code in parallel.

Dart is type safe, which means that a variable's value always matches its static type, which results in fewer runtime errors in production. However the type system is flexible, allowing us to use dynamic types and runtime checks when required. It also provides null safety which means that values cannot be null unless explicitly allowed.

## Dart CLI
`dart analyze`   Analyze Dart code in a directory.
`dart compile`   Compile Dart to various formats.
`dart create`    Create a new Dart project.
`dart fix`       Apply automated fixes to Dart source code.
`dart format`    Idiomatically format Dart source code.
`dart migrate`   Perform null safety migration on a project.
`dart pub`       Work with packages.
`dart run`       Run a Dart program.
`dart test`      Run tests for a project.dart 


## Variables
To check type:
- `is` operator (`((num1 + num2) is int);`)
- `runtimeType` (`((num1 + num2).runtimeType);`)

String interpolation:
- `print('The type of $var_name is a String?');`
- `print('The type of $var_name is a String? ${var_name is String}');` <-- can add more complex expressions

Type annotation:
- Can annotate type as `String var_name = "hello_world"`
- Dart automatically infers `var name = "string";` as string type, however we can explicitly type it as `String name = "string;` 
- `var` keyword --> Dart assigns type by inference
- `final` marks variables that cannot be reassigned
- `const` creates an immutable compile time constant --> value needs to be known at compile time
- `const` is more performant than `final`

## Null Safety
Null Safety was introduced in version 2.

By default a variable cannot be assigned a `null` value. If you want a variable to be able to have value `null` you need to declare it with the sign `?`:
- `int? age;` <-- we do not need to explicily assign null
- However we cannot assign a nullable variable to a non-nullable variable by default
- In order to do that Dart provides the assertion operator `!` to make the compiler think that the value is non-null (e.g. `String non_null_var = nullable_var!;`), however this increases the risk of runtime errors
- In classes it is commong to have variable declaration before assignment, so how can we make variables  non-nullable? We can declare them with the `late` keyword (e.g. `late final String _size;`)

## Object-Orientation
In Dart anything we can store in a variable is an object, and every object is an instance of a class. The only thing that is not an ob ject in Dart is `null`. This opens the door to multiple paradigmns:

- Functions are first-class objects , therefore they can be passed around for functional programing, through annonymous arrow functions
- Define classes with mixin based inheritance for object oriented patterns. For more check [here](https://stackoverflow.com/questions/53699482/what-is-mixin-based-inheritance-in-dart/56057529)


## Control Flow

## Loops:
- for loop:
```
for (var i = 0; i < 5; i++) {
  print(i)
  // break <- breaks the loop
  // continue <- skips an iteration of the loop
}
```
- while loops:
```
int i = 0;
while (i < 5) {
  print(i)
  i++;
}
```
- do while loops:
```
i = 0;
do {
  print(i);
} while (i < 5);
```

## Conditionals:

Standard conditional:
```
if (color == 'blue') {
  //
} else if (color == 'green') {
  //
} else {
  // default
}
```

Simple conditionals:
You can omit the curly braces and put everything in a single lign.
`if (color == 'red') print('hello red');`


Differences with JavaScript:
- In JS we can check the if a string is empty by `if (thing1);`. However in Dart you need to actually check that it's empty by doing `if(thing1.isEmpty);`
- In JS when you pass `null` to a `bool` it defaults to `false`. Thius does not happen in Dart. If you need to explicilty check if a value is null in dart --> `if (thing2 != null);`


Assert:
Assert is a funciton that takes a condition as an argument and if that condition is true nothing happens but if it's false it will raise an error. However the error is only raised in `debug mode`. In production mode the error will be ignored. It's a way to evaluating the shape of data before operating on it further in the code.


## Operators
- And operator `&&`
- Or operator `⁄⁄`
- Increment/Decrement operator `++`/`--`
- Assign-if-null Operator `??=` --> (`name ??= 'Guest';` or `var z = name ?? 'Guest';`)
- Ternary operator: `var isThisBlue = (color == 'blue') ? 'Value if blue' : 'Value if not blue';`

Ternary operator is very useful in flutter because it helps building the UI based on different state changes to the application data

- Cascade operator:

Without the cascade operator:
```
dynamic Paint;

var paint = Paint();
pain.color = 'black';
pain.strokeCap = 'round';
pain.strokeWidth = 5.0;
```

With cascade operator:
```
dynamic Paint;

var paint = Paint()
  ..color = 'black'
  ..strokeCap = 'round'
  ..strokeWidth = 5.0;
```

- Typecast `as` operator allows to cast types (e.g. `var number = 23 as String;`)


## Functions
Functions are first class objects which means they can be assigned to variables and passed as arguments or return values from other functions which makes it possible to implement functional programming patterns.

In Dart there is no function keyword. To define a function simply decide on a name and add `() {}` on it:

```
myFunction() {
  ///
}
```

To Call the function we can simply call it:
`myFunction();`

Dart can do infer the type of the output, however we can strongly type the function output:
```
String myFunction() {
  return '';
}
```

To add positional parameters to a function:
```
String myFunction(int number) {
  return '$number';
}
```

To add keyword/named parameters to a function (adding braces around it):
```
String myFunction({ int number1 }) {
  return '$number1';
}
```

However the curly braces make the parameters optional. To make them mandatory inside the curly braces:
```
String myFunction({ required int number1 }) {
  return '$number1';
}
```

To add a default value to a parameter:
```
String myFunction({ int number1 = 5 }) {
  return '$number1';
}
```

Arrow Functions:
Instead of using curly braces we can do `myFunction(int number) => '$number';` , therefore we can write functions as a one-liner. This comes really handy when passing functions as arguments, which comes into play all the time when working with flutter, such as on click functions.

Annoymous Functions:
We can create annonymous arrow functions: 
`() => 'hello_world'`

CallBack functions:
Many APIs in Dart use callback functions, often to handle events or gestures in Flutter:

```
callIt(Function callback) {
  var result = callback();

  return 'Result $result';
}
```


## Lists (Arrays)
- A list/array inherits from the class Iterable
- Most commong Iterables: Lists, Map, Set
- When defining a list we can add a generic type using `<>` (e.g. `List<int> list = [1, 2, 3, 4];`)
- Accessing individual items on a list -> `list[0];`
- Access mutliple items at a time -> `list.sublist(2, 5);` where `2` and `5` are the start and end index
- Creating a list without the literal syntax -> `var list2 = List.filled(50, 'hello');`
- Get the total size of a list -> `list.length;`
- First and last properties -> `list.first;` and `list.last;`
- To push an item into the end of the list -> `list.add(4);`
- To pop an item from the end of the list -> `list.removeLast();`
- Insert an item in a given index -> `list.insert(1, 1000);`
- Looping through a list:

```
for (int n in list) {
  print(n);
}
```

or a more functional programming approach:
`list.forEach((n) => print(n));`

another looping method:
`var doubled = list.map( (n) => n*2 );`

Map is incredibly useful as well because often we have a list of data that we need to map onto a list of UI widgets.

- Combine multiple lists together using spread syntax (three dots):
`var combined = [...list1, ...list2]`

- We can use conditional logic directly inside the literal syntax:

```
bool depressed = false;
var cart = ['milk', 'eggs', if (depressed) 'Vodka'];
```

## Maps (Dictionaries)
- Hashmap or Dictionary (Key-value pair)
- Also has Generic typic -> `Map<String, dynamic> book = {};` where `String` is the Key Type and `dynamic` the value type
- Access value in the map -> `book['title'];`
- Access keys or values as iterable -> `book.keys;` or `book.values;`
- Convert iterable to list -> `book.values.toList();`
- Loop through the map:

With standard loop:
```
for (MapEntry b in book.entries) {
  print('Key ${b.key}, Value ${b.value}');
}
```

With forEach method:
`book.forEach((k, v) => print('Key ${b.key}, Value ${b.value}'));`


## Classes
- To create a custom class:

```
class Basic {

}
```
- To instanciate a class -> `Basic thing = new Basic();` or simply `Basic thing = Basic();`
- To create instance variables/class atributes:

```
class Basic {
  int id;

Basic(this.id); // this is a constructor
}
```

And then to instanciate -> `Basic thing = Basic(5);` to give id the value of 5

- To create a method:
```
class Basic {
  int id;

  Basic(this.id); // this is a constructor

  doStuff() {
    print("Hello my ID is $id");
  }
}
```

- To create static methods (functions that instead of operating on a class instance they operate globally):
```
class Basic {
  int id;

  Basic(this.id); // this is a constructor

  static helper_func() {
      //
  }
}
```

We can then call the method as such -> `Basic.helper_func()` as we do not require an instance. This can be useful when we want to have a global helper method that doesn't rely on the internal state of an individual object.

### Constructors
- Construcot allows us to pass data into a class when an object is created and can also allow us to run initialisation logic.

```
class Rectangle {
  final int width;
  final int height;

  Rectangle(this.width, this.height)
}
```

If we want to calculate a variable upon initialisation that is a combination of the attributes inputed:

```
class Rectangle {
  final int width;
  final int height;
  late final int area;

  Rectangle(this.width, this.height) {
      area = width * height; // the keyword .this is optional
  }
}
```
- When referring to class attributes, the keyword `this` is optional, therefore we technically need only to use it to avoid name collision
- We can add additional arguments to the constructor that are optional, by declaring a nullable variable and adding it to the Constructor parameters under brackets:

```
class Rectangle {
  final int width;
  final int height;
  late final int area;
  String? name;

  Rectangle(this.width, this.height, [this.name]) {
      area = width * height; // the keyword .this is optional
  }
}
```
- The vast majority of classes in Dart will use named arguments instead of positional arguments:

We can do that by adding the variables to the constructor inside curly braces. By doing that we do not need to the declare them outside the constructor. By default a named parameter will be optional so we can sue the keyword `required`. using the `const` keyword in the constructor also allows us to instanciate objects with the `const` keyword.
```
class Circle {

  const Circle({ requiredint radius, String? name });

}
```

-  We can also create named constructors:

```
class Point {
  double lat = 0;
  double lng = 0;

  // Named constructor
  Point.fromMap(Map data) {
    lat = data['lat'];
    lng = data['lng'];
  }

  // fromList constructor
  Point.fromList(List data) {
    lat = data[0];
    lng = data[1];
  }
}
```


### Interface
- Whenever we create a class in Dart we are also implicitly creating an interface
- An interface determines how the class will look to someone else using it in the codebase
- It determines what other developers will see in the InteliSense when working with the class in a different file
- By default instance attributes and methods are public
- To create a private member that is only available on the class implementation itself by naming variables or methods starting with an underscore -> `final int _id = 23;` or `_saySecret() => 'My ID is $id.';`
- When implementing the class you will still have access to the values, but as the class is imported into a different file they will not be visible in the InteliSense and the compiler will throw an error if you try to access them
- Constructors are also not available to the interface
- We can also create an abstract class `abstract class Elephant {}` which creates a class that cannot be instanciated

### Inheritance
- The superclass or parent class contains behavious that are shared by all subclasses. The `abstract` keyword is used to indicate that the class is not meant to be instanciated but rather to be inherited from.
- Subclasses can overrride the behaviour of the superclass by implementing the `@override` decorator
- To Inherit from a parent class use the keyword `extends` and to override functionality the decorator `@override` :
  
```
class GreenFrog extends StatelessWidget {
  const GreenFrog({ Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Container(color: const Color(0xFF2DBD3A));

  }
}
```
- To use the initial functionality of the parent we use the keyword `super`:

```
class Pub extends Dog {
  String breed = 'pug';

  @override
  void walk() {
      super.walk();
      print("I am tired. Stopping now.);
  }

}
```


### Mixins
- In some cases extending a class is not enough and we may want to add additional behaviours beyond the initial extension
- For that we can create mixins, which can be very powerful for more complex projects
- We use the keyword `with` to extend a class with mixins


```
mixin Strong {
  bool doesLift = true;

  void benchPress() {
      print('doing bench press...);
  }
}

mixin Fast {
  bool doesRun = true;

  void benchPress() {
      print('running fast...);
  }
}

class SuperHuman extends Human with Strong, Fast {
  //
}

```

### Generics
- A generic is a way to pass a type -> `List<int> numbers = [1, 2, 3];`
- A List is like a container that can hold many different types of things.
- A generic type provides a way to strongly type things inside of that container
- We can create out out generic implementation :

```
class Box<T> {
  // T represents a variabgle type that can be anything passed in by the user when instanciating
  // This allows us to use T inside of the class definition

  T value;

  Box(this.value);

  T openBox() {
      return value;
  }
}

// to instanciate
Box<String> box1 = Box('Cool thing);
```

## Packages
- Standard import -> `import 'package:sign_in_with_apple/sign_in_with_apple.dart';`
- If there are name collisions Dart will prioritise the namespace of the file
- To use a custom name -> `import 'package:sign_in_with_apple/sign_in_with_apple.dart' as apple_sign;`
- To omit an object/class -> `import 'package:sign_in_with_apple/sign_in_with_apple.dart' hide signInWithApple;`
- To import only an object/class -> `import 'package:sign_in_with_apple/sign_in_with_apple.dart' show signInWithApple;`
- An import from Dart native modules -> `import 'dart:math';`
- An import from pub.dev will start with `package:`


## Asynchronous Code
### Futures
- Futures are very similar to promises
- Need to import library `ìmport 'dart:async';`
- Future allows to perform an operation in the background (i.e. read from a cloud database)
- Dart implements an Event Loop that allow certain things to be queued up in the background and then handled later with a callback function
- A Future is a one-time event
- "Promise" Syntax:

The function `then` and `catchError` are mutually exclusive.
```
var delay = Future.delayed(Duration(seconds: 5));

delay
  .then( (value) => print('I have been waiting') )
  .catchError( (err) => print(err) );
```

- Dart supports `async-await` syntax, making the code more sync-like:

It replaces `then` and `catch` with `async` and `await`. The keyword `async` in a function will tell Dart to automatically return a Future and then we can use the `await` keyword inside the function body which will pause the execution of the function until the promise in front of it resolves. This eliminates the need to use `then` along with the callback function.
```
Future<String> runInTHeFuture() async {
  var data = await Future.value('world');

  return 'hello $data';
}
```

### Streams
- Streams allows us to handle multiple asynchronous events and handle them from the same place as they unfold over time (i.e. listening to a real-time data source like firebase firestore, or a websocket connection)
- We can create a Stream using the `Stream` class, then call its `fromIterable` constructor to create a stream of events `var stream = Stream.fromIterable([1, 2, 3]);`
- In the real world the events are often separated by long time intervals
- To listen to the stream using its `listen` method, which takes a callback function that will be executed for every event that is emitted by the stream --> `stream.listen( (event) => print(event) );`
- Another way of thinking of Streams is to thinkof a List that unfolds over the dimension of time
- A Stream as many of the events that we can find on a List, like `map`
- A Stream can only be listen to one time

```
void main() {
  var stream = Stream.fromIterable([1, 2, 3]);

  stream
    .map( (event) => event * 2 )
    .listen( (event) => print(event) );
}
```

- The default behaviour is that a Stream can only be listened to one time
- To have multiple listeners we can turn the stream into a Broadcast Stream -> `var stream = Stream.fromIterable([1, 2, 3]).asBroadcastStream();`

Example of a stream with two `listen`
```
void main() {
  var stream = Stream.fromIterable([1, 2, 3]);

  stream.listen( (event) => print(event) );

  stream
    .map( (event) => event * 2 )
    .listen( (event) => print(event) );
}
```

- We can also use `async-await` syntax with Streams. Since we are dealing with multiple values we will await a for loop:
```
streamFun() {
  var stream = Stream.fromIterable([1, 2, 3]);

  await for (int value in stream) {
    // this code will execute each time an event is emitted
    print(value);
  }
}
```
