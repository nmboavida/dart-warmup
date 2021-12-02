## dart-warmup

Type-safe general purpose programming language designed for building fast apps on multiple platforms.

Was supposed to be an alternative to Javascript but was not really embrassed by the Web development community. It bounced back and was adopted by the Flutter framework.

It's unique in its ability to compile to multiple targets:
- ARM64 machine code for mobile devices
- Javascript for Web Browsers
- Self contained executables (i.e. x86_64) for Widnows, MacOs, Linux

Has a JIT compiler which compiles source code to machine code on the fly, which can boost developer productivity with features like hot-reload in Flutter.

All Dart code runs inside of an `isolate` which is a chunk of memory running in a single threaded event-loop, which makes it possible to perform asynchronous background work on a single thread. Dart also allows us to spaw multiple isolates to run code in parallel.

Dart is type safe, which means that a variable's value always matches its static type, which results in fewer runtime errors in production. However the type system is flexible, allowing us to use dynamic types and runtime checks when required. It also provides null safety which means that values cannot be null unless explicitly allowed.

### Typing
`var name = "string";`
Dart automatically infers this as string type, however we can explicitly type it as:
`String name = "string;`


### Object-Oritation
In Dart anything we can store in a variable is an object, and every object is an instance of a class. The only thing that is not an ob ject in Dart is `null`. This opens the door to multiple paradigmns:

- Functions are first-class objects , therefore they can be passed around for functional programing, through annonymous arrow functions
- Define classes with mixin based inheritance for object oriented patterns. For more check [here](https://stackoverflow.com/questions/53699482/what-is-mixin-based-inheritance-in-dart/56057529)
