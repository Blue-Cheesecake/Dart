# Dart

Just use for review Dart.

## Getting started

Since Dart programming language is popular for building mobile applications with Flutter software development kit, the installation of dart will come along with installation of flutter

### Installing Dart

The installation on different operating system can be easy followed via <a href="https://docs.flutter.dev/get-started/install">Flutter Documentation Installation</a>

1. You need to get the archive of Flutter via downloading directly or using git
2. Extract the archive, and permanently update PATH in your local machine. (The ways to update PATH is different on each different OS. Please follow the instruction of Flutter document)

After installing Flutter, you should be able to run Dart command.

Type the following command to check whether Dart command is installed

```
$ dart --version
```

It should look like this

```
$ dart --version
Dart SDK version: 2.17.0 (stable) (Mon May 9 10:36:47 2022 +0200) on "macos_arm64"
```

The version and OS might be different depending on what you have installed and your OS.
It's not look like this, please go back, and strictly try again given by the official Flutter documentation.

### Downloading IDE

The recommended IDE from my opinion is **vscode** can be downloaded via <a href="https://code.visualstudio.com/download">This Link</a>

Install, **Dart**, and **Flutter** extensions.

## What you will learn

- Basic Concept of Dart.
- Data types
- Variable declaration
- If statement
- Loops
- Function
- **Class**
  - Attribute
  - Static
  - Methods
  - Factory
  - Custom operation
  - Inheritance

### Basic

You need to create main function. Dart will run **only** **main** function.

Always add semicolon `;` after end line **except** **curly brackets**

```dart
void main() {
  print("Hello World");
}
```

use **print** function to display any message in the console.

### Data Types

- Null
- Object

  - Numbers: `num` can be either integer or double
    - Integer: `int`
    - Double: `double`
  - Strings: `String` is any message surrounded by single or double quote.

    - We can include variable by using dollar `$` sign like this -> `"my name is: $name"` or `"my name is: ${name}"`
    - The difference between single dollar and dollar followed by curly bracket is single dollar can only include 1 variable but has no any operation but dollar followed by curly bracket can include any operator
    - For example

      ```dart
      void main() {
        String firtname = "Sinut";
        String lastname = "Wattanarporn";
        print("full name: ${firtname + lastname}"); // SinutWattanarporn
      }
      ```

  - Boolean: `bool` can be either `true` or `false`

  - Iterable: `Iterable<T>`
    - List: `List<T>`, a collections of data. Replace `T` with other data types.
    - Set: `Set<T>`, a collection of data with set format. Replace `T` with other data types
    - Maps: `Map<T, T>`, a collection of pairs. Replace `T` with other data types.
    - Dynamic: `dynamic`: a special data type which can be any data type

### Declaration & Initialization

Dart can declare and initialize later or declare with initialize together.

There are 4 keywords for declaration in Dart

- `var`
  - normally use for variable potentially needed to reassigned later.
  - simple data which once initialized, it can't be changed data type.
  - **can** be **reassigned** at anytime.
- `final`
  - normally use for `List`, `Set`, `Map`
  - **can't** be **reassigned** anymore.
  - can add new value inside it.
- `const`
  - normally use for the fact variable for making it constant such as PI value which is 3.14
  - **can't** be **reassigned** anymore.
  - **can't** be **change** its value.
- `late`
  - must use along side with `var`, `final`, `const` or explicit type.
  - declare variable that will be initialized after declaration.
- Explicit data type (eg. `num`, `String`, `Set<int>`, etc.)
  - Conventionally use `var` instead of explicit type.
  - use along side with `final`, `late`, or `const` since it will be that exact data type.

## Type checking

using `is` keyword.
or using `.runtimeType` to review its type.

```dart
void main(List<String> args) {
  final map = <int, String>{};
  print(map is Map); // true
  print(map.runtimeType); // _InternalLinkedHashMap<int, String>
}
```

## Null Safety

Null mean nothing. We can assign the null value by using explicit type followed by question mark `?` sign.

For example,

```dart
String? foo = null;
```

It means that `foo` variable can be either `null` or `String` type.

<hr>

## Function

declare the type of variable that function will return. `void` for nothing.
Declare the explicit type of parameter.

```dart
int foo(int x) {
  return x + 1;
}

String fullName(String firstName, String lastName) {
  return "$firstName $lastName";
}

void baz() {
  print("Hello World");
}
```

## Object oriented programming

### Class

### Optional Parameters constructor

### Factory

### Custom Operator

### Inheritance

### Examples

for Optional Operator, Factory, Method, and Custom operator.

```dart
class Vector3D {
  double _x, _y;
  double? _z;

  // Optional constructor
  Vector3D(this._x, this._y, [this._z]);

  // Factory constructor
  factory Vector3D.same(double u) {
    return Vector3D(u, u, u);
  }

  // Method
  bool coincide(Vector3D other) {
    if (other._x / this._x == other._y / this._y &&
        other._y / this._y == other._z! / this._z!) return true;
    return false;
  }

  // Custom operator
  @override
  bool operator ==(covariant Vector3D other) {
    return other._x == this._x && other._y == this._y && other._z == this._z;
  }

  Vector3D operator +(Vector3D other) {
    return Vector3D(_x + other._x, _y + other._y, _z! + other._z!);
  }
}

void main(List<String> args) {
  final Vector3D a = Vector3D(2, 1, 3);
  final Vector3D b = Vector3D(2, 2, 6);
  final Vector3D c = Vector3D.same(2);
  final bool ret = a == b;
  print("a does equals to b?: $ret");
  final Vector3D ab = a + b;
  print("a + b: ${ab._x} ${ab._y} ${ab._z}");

  print(c._x);
  print(c._y);
  print(c._z);
  print(a.coincide(b));
}
```

for abstract class, Future, extends, getter, setter, async, and await.

```dart
// Abstract
abstract class GroceryAction {
  Future<void> goToGroceryStore() {
    print("Going to grocery\n.\n.");
    return Future.delayed(const Duration(seconds: 3), () {
      print("Reached Grocery store!!");
      print("__________________");
    });
  }

  Future<void> buyMilk() {
    print("Going to buy milk\n.");
    return Future.delayed(const Duration(seconds: 2), () {
      print("Grabbed Milk!");
      print("__________________");
    });
  }
}

// Extending
class Person extends GroceryAction {
  late String firstName;
  late String lastName;
  late int _age;

  Person(String fn, String ln, int age) {
    firstName = fn;
    lastName = ln;
    setAge(age);
  }

  factory Person.android() => new Person("Foo", "Bar", 0);

  // getter & setter
  int get getAge => _age;
  void setAge(int value) {
    // validate
    if (value < 0 || value >= 100) {
      // throw error
      throw new Error();
    }
    _age = value;
  }

  // Async & Await
  void goToBuyMilk() async {
    await this.goToGroceryStore();
    await this.buyMilk();
    print("__________________");
    print("End");
    print("__________________");
  }
}

extension Police on Person {
  void fireGun() => print("Bang!!");
}

void main(List<String> args) {
  final baz = Person.android();
  print(baz.getAge);
  baz.setAge(10);
  print(baz.getAge);
  baz.fireGun();
  baz.goToBuyMilk();
}
```

### Extensions

### Getter & Setter

not usually be used

```Dart
T get getName => attribute
void sét setName(T arg) {
  this.arg = arg
}
```

### Future & async await

The future function, if we need to use async before function and await when calling that function in order to get data from future function, it will return future object otherwise.

```Dart
Future<T> functionName(T foo) {
  return Future.delayed(const Duration(seconds: 3), () {
    return [result from operated foo]
  });
}
```

### Stream

Continue compute and return value into pipe
pipe if data that either complete or never complete [loop forever]
A pipe of future that send down to pipe

```Dart
Stream<T> funcName() {
  return Stream.value(T val);
}

Stream<T> periodicFunc() {
  return Stream.periodic(const Duration(seconds: 1), (value) {
    return T value;
  });
}

// using

await for (final value in funcName()) {
  print(value);
}
```

### Generators

a function that return a list of things but it internally compute data in simple way

`sync*` -> async generator function return iterable and compute value inside them synchronously
`async*` -> return Stream, compute synchronously

use yield in Generator function

```Dart
Iterable<T> funcName() sync* {
  yield 1;
  yield 2;
  yield 3;
}

const a = funcName(); // get collection of 1, 2, 3 [1, 2, 3]

// loop over function
for (final value in funcName()) {
  print(value);
}
```

### Generics

```Dart
class Pair<A, B> {
  final A value1;
  final B value2;
  Pair(this.value1, this.value2);
}
```

## References

- <a href="https://dart.dev/guides/language/language-tour">Overall</a>: This helped me to walkthrough the overall concept of dart.

- <a href="https://dart.dev/null-safety/understanding-null-safety">Null Safety</a>: Provide full details of null safety.

- <a href="https://stackoverflow.com/questions/52449508/constructor-optional-params">Optional Constructor</a>
