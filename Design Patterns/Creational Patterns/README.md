### Resource for creational patterns by [Kamran Ahmed](https://github.com/kamranahmedse/design-patterns-for-humans#creational-design-patterns)

# Singleton

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
