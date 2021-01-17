### Resource for creational patterns by [Kamran Ahmed](https://github.com/kamranahmedse/design-patterns-for-humans#creational-design-patterns)

# 1. Singleton
**Singleton** is a creational design pattern that lets you ensure that a class has only one instance, while providing a global access point to this instance.

**Reading Resources**
- [Flutter Design Patterns: 1 — Singleton by Mangirdas Kazlauskas](https://medium.com/flutter-community/flutter-design-patterns-1-singleton-437f04e923ce)
- [Singleton by Refactoring Guru](https://refactoring.guru/design-patterns/singleton)

```dart
void main() {
  final s1 = Singleton();
  print('Singleton: ${s1.hashCode}');
​
  final s2 = Singleton();
  print('Singleton: ${s2.hashCode}\n');
​
  final ls1 = LazySingleton();
  print('Lazy Singleton: ${ls1.hashCode}');
​
  final ls2 = LazySingleton();
  print('Lazy Singleton: ${ls2.hashCode}');
}
​
class Singleton {
  Singleton._();
​
  static final _instance = Singleton._();
​
  factory Singleton() {
    return _instance;
  }
}
​
class LazySingleton {
  LazySingleton._();
​
  static LazySingleton _instance;
​
  factory LazySingleton() {
    if (_instance == null) {
      _instance = LazySingleton._();
    }
​
    return _instance;
  }
}
```

# 2. Factory Method (Virtual Constructor)
**Factory Method** is a creational design pattern that provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created.

**Reading Resources**
  - [Factory Method by Refactoring Guru](https://refactoring.guru/design-patterns/factory-method)
  - [Flutter Design Patterns: 10 — Factory Method by Mangirdas Kazlauskas](https://mkobuolys.medium.com/flutter-design-patterns-10-factory-method-c53ad11d863f)

```dart
void main() {
  Shape shape = ShapeFactory.buildShape(ShapeType.circle);
  shape.draw();

  shape = ShapeFactory.buildShape(ShapeType.square);
  shape.draw();
}

enum ShapeType { circle, square }

class ShapeFactory {
  static Shape buildShape(ShapeType shapeType) {
    switch (shapeType) {
      case ShapeType.circle:
        return Circle();
      case ShapeType.square:
        return Square();
      default:
        throw FormatException('This Shape not implemented');
    }
  }
}

abstract class Shape {
  void draw();
}

class Circle implements Shape {
  @override
  void draw() => print('drawing Circle');
}

class Square implements Shape {
  @override
  void draw() => print('drawing Square');
}
```

# 3. Abstract Factory (Kit)
**Abstract Factory** is a creational design pattern that lets you produce families of related objects without specifying their concrete classes.

**Reading Resources**
  - [Abstract Factory by Refactoring Guru](https://refactoring.guru/design-patterns/abstract-factory)
  - [Flutter Design Patterns: 11 — Abstract Factory by Mangirdas Kazlauskas](https://medium.com/flutter-community/flutter-design-patterns-11-abstract-factory-7098112925d8)

```dart
void main() {
  final materialFactory = MaterialFactory();
  final materialButton = materialFactory.makeButton();
  final materialCheckBox = materialFactory.makeCheckBox();

  materialButton.onTap();
  materialCheckBox.onTap();
  materialCheckBox.onTap();

  print('\n');

  final cupertionFactory = CupertinoFactory();
  final cupertionButton = cupertionFactory.makeButton();
  final cupertionCheckBox = cupertionFactory.makeCheckBox();

  cupertionButton.onTap();
  cupertionCheckBox.onTap();
  cupertionCheckBox.onTap();
}

/// Material Factory for Material Widgets
class MaterialFactory implements WidgetsFactory {
  @override
  Button makeButton() => MaterialButton();

  @override
  CheckBox makeCheckBox() => MaterialCheckBox();
}

/// Cupertino Factory for Cupertino Widgets
class CupertinoFactory implements WidgetsFactory {
  @override
  Button makeButton() => CupertinoButton();

  @override
  CheckBox makeCheckBox() => CupertinoCheckBox();
}

abstract class WidgetsFactory {
  Button makeButton();

  CheckBox makeCheckBox();
}

/// For Button
abstract class Button {
  String get title;

  void onTap() => print('$title tapped!');
}

class MaterialButton extends Button {
  @override
  String get title => 'Material Button';
}

class CupertinoButton extends Button {
  @override
  String get title => 'Cupertino Button';
}

///For CheckBox
abstract class CheckBox {
  String get title;

  bool checked = false;

  void onTap() {
    checked = !checked;
    print('$title checked: $checked');
  }
}

class MaterialCheckBox extends CheckBox {
  @override
  String get title => 'Material CheckBox';
}

class CupertinoCheckBox extends CheckBox {
  @override
  String get title => 'Cupertino CheckBox';
}

```

# 4. Prototype (Clone)
**Prototype** is a creational design pattern that lets you copy existing objects without making your code dependent on their classes.

**Reading Resources**
  - [Prototype by Refactoring Guru](https://refactoring.guru/design-patterns/prototype)
  - [Flutter Design Patterns: 14 — Prototype by Mangirdas Kazlauskas](https://medium.com/flutter-community/flutter-design-patterns-14-prototype-7d7d18bcf643)

```dart
void main() {
  final c1 = Circle('black', 10);
  final c2 = c1.clone() as Circle;
​
  print('c2 radius: ${c2.radius}');
  print('c2 color: ${c2.color}');
  
  print('\n');
​
  final r1 = Rectangle('red', 10, 15);
  final r2 = r1.clone() as Rectangle;
​
  print('r2 color: ${r2.color}');
  print('r2 height: ${r2.height}');
  print('r2 width: ${r2.width}');
}
​
abstract class Shape {
  String color;
​
  Shape(this.color);
​
  Shape.clone(Shape source) {
    color = source.color;
  }
​
  Shape clone();
}
​
class Circle extends Shape {
  double radius;
​
  Circle(String color, this.radius) : super(color);
​
  /// returns new object
  Circle.clone(Circle source) : super.clone(source) {
    radius = source.radius;
  }
​
  @override
  clone() => Circle.clone(this);
}
​
class Rectangle extends Shape {
  double height;
  double width;
​
  Rectangle(String color, this.height, this.width) : super(color);
​
  /// returns new object
  Rectangle.clone(Rectangle source) : super.clone(source) {
    height = source.height;
    width = source.width;
  }
​
  @override
  clone() => Rectangle.clone(this);
}
```

# 5. Builder
**Builder** is a creational design pattern that lets you construct complex objects step by step. The pattern allows you to produce different types and representations of an object using the same construction code.


**Reading Resources**
  - [Builder by Refactoring Guru](https://refactoring.guru/design-patterns/builder)
  - [Flutter Design Patterns: 18 — Builder by Mangirdas Kazlauskas](https://medium.com/flutter-community/flutter-design-patterns-18-builder-cdc90b222724)



