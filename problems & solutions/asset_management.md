# Title: Managing Assets in Flutter

## Problem
In a Flutter project, managing a growing set of SVG icons efficiently became a challenge. Initially, a switch statement was used to handle SVG icon paths, but this approach quickly became unwieldy as the number of icons increased. This document outlines the initial approach, the problems encountered, and the evolution of the solution.


## Initial Approach
### *Switch Statment*
```dart
  String getIconPath(String iconName) {
  switch (iconName) {
    case 'add':
      return 'assets/svgicons/add.svg';
    // Other cases...
    default:
      return '';
  }
}
```
### Benefits:

**Simplicity:**<br> Easy to understand and implement for a small number of cases.<br>

**Direct Mapping:**<br> Directly maps string values to paths with straightforward logic.<br>

### Drawbacks:

**Code Duplication:**<br> Each new icon requires adding a new case, leading to repetitive code.<br>

**Maintainability Issues:**<br> As the number of icons grows, the switch statement becomes cumbersome and harder to manage.<br>

**Scalability Problems:**<br> Not suitable for large or dynamic sets of icons. Adding or removing icons requires modifying the switch statement.<br>

#### *Static Getters*
```dart
  class SvgIcons {
  static String get add => 'assets/svgicons/add.svg';
  // Other static getters...
}
```
### Benefits:

**Readability:** <br>Provides a clean and readable way to access icon paths.<br>

**Direct Access:**<br> Each icon path is accessed through a specific getter, making it easy to understand which path is being used.<br>

### Drawbacks:

**Boilerplate Code:**<br> Requires a separate static getter for each icon, leading to a lot of boilerplate code as the number of icons grows.<br>

**Limited Flexibility:**<br> Adding new icons still requires updating the class with new getters, which is not as flexible or scalable as other methods.<br>


### Final Solution
#### *Map Lookup*
```dart

class SvgIcons {
  static const String _basePath = 'assets/svgicons/';

  static const Map<String, String> _icons = {
    'add': '${_basePath}add.svg',
    // Additional icons...
  };

  static String getIconPath(String iconName) {
    return _icons[iconName] ?? '';
  }
}
```

### Benefits:

**Scalability:** <br> Easily handles a large number of icons. Adding or removing icons involves simple modifications to the map.<br>

**Maintainability:**<br> Reduces code duplication and complexity. The map structure allows for centralized management of icon paths.<br>

**Flexibility:**<br> Adding new icons requires only updating the map, making it a flexible solution that can grow with the project.<br>

### Drawbacks:

**Initial Setup:**<br> Requires setting up a map and managing its contents, which may be more complex initially.<br>

**Performance:**<br> While typically negligible, map lookups might have slightly higher overhead compared to direct static lookups, though this is generally not a concern for most applications.<br>

**Conclusion:**

Each approach has its own benefits and drawbacks. The switch statement is simple but lacks scalability. Static getters improve readability but lead to boilerplate code.Then i chose The map lookup  solution provides a scalable and maintainable approach suitable for managing a large number of assets efficiently.
