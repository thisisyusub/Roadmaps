### Resource for creational patterns by [Kamran Ahmed](https://github.com/kamranahmedse/design-patterns-for-humans#creational-design-patterns)

# 1. Singleton

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
