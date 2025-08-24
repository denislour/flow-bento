# Symbol Kinds Reference

## Overview
This document provides a comprehensive reference for Language Server Protocol (LSP) symbol kinds used throughout Flow-Bento development tools. Understanding these kinds is essential for effective symbol filtering and analysis.

## Standard Symbol Kinds

### **Kind 1: File**
- **Description**: Represents a file entity
- **Usage**: File-level symbols, typically used in workspace symbol searches
- **Example**: `main.py`, `config.json`
- **Filter Usage**: `include_kinds=[1]` to find files only

### **Kind 2: Module** 
- **Description**: Module or namespace declarations
- **Usage**: Python modules, JavaScript modules, namespaces
- **Example**: 
  ```python
  # Python module
  import user_service
  
  # Namespace in other languages
  namespace MyApp.Services
  ```
- **Filter Usage**: `include_kinds=[2]` for modules only
- **Common Exclusion**: `exclude_kinds=[2]` to skip import statements

### **Kind 5: Class**
- **Description**: Class definitions
- **Usage**: Object-oriented programming class declarations
- **Example**:
  ```python
  class UserService:
      pass
  
  class DatabaseConnection:
      pass
  ```
- **Filter Usage**: `include_kinds=[5]` for classes only
- **Most Common**: Primary target for code structure analysis

### **Kind 6: Method**
- **Description**: Methods within classes
- **Usage**: Class member functions, instance methods
- **Example**:
  ```python
  class User:
      def login(self, password):    # Method
          pass
      
      def get_name(self):          # Method
          pass
  ```
- **Filter Usage**: `include_kinds=[6]` for methods only
- **Note**: Distinguished from standalone functions (kind 12)

### **Kind 9: Constructor**
- **Description**: Class constructors and initializers
- **Usage**: Object initialization methods
- **Example**:
  ```python
  class User:
      def __init__(self, name):    # Constructor
          self.name = name
  ```
- **Filter Usage**: `include_kinds=[9]` for constructors only
- **Language Specific**: `__init__` in Python, constructors in other languages

### **Kind 12: Function**
- **Description**: Standalone functions (not class members)
- **Usage**: Module-level functions, utility functions
- **Example**:
  ```python
  def process_data(data):          # Function
      return data.strip()
  
  def calculate_score(x, y):       # Function
      return x + y
  ```
- **Filter Usage**: `include_kinds=[12]` for functions only
- **Distinction**: Not bound to any class (vs methods)

### **Kind 13: Variable**
- **Description**: Variable declarations and assignments
- **Usage**: Module-level variables, class attributes
- **Example**:
  ```python
  DATABASE_URL = "localhost"       # Variable
  
  class Config:
      debug_mode = True           # Variable (class attribute)
  ```
- **Filter Usage**: `include_kinds=[13]` for variables only
- **Scope**: Can be local, instance, or class-level

### **Kind 14: Constant**
- **Description**: Constants and immutable values
- **Usage**: Configuration values, enum values, final variables
- **Example**:
  ```python
  MAX_RETRY_COUNT = 3             # Constant
  API_VERSION = "v1.0"            # Constant
  
  class Colors:
      RED = "#FF0000"             # Constant
  ```
- **Filter Usage**: `include_kinds=[14]` for constants only
- **Convention**: Often UPPERCASE in Python

## Extended Symbol Kinds

### **Kind 3: Namespace**
- **Description**: Namespace declarations
- **Usage**: Language-specific namespacing constructs
- **Less Common**: In Python projects

### **Kind 4: Package**
- **Description**: Package-level symbols
- **Usage**: Package imports and declarations
- **Example**: `from mypackage import module`

### **Kind 7: Property**
- **Description**: Properties and getters/setters
- **Usage**: Class properties, computed attributes
- **Example**:
  ```python
  class User:
      @property
      def full_name(self):         # Property
          return f"{self.first} {self.last}"
  ```

### **Kind 8: Field**
- **Description**: Class fields and member variables
- **Usage**: Instance variables, class variables
- **Example**:
  ```python
  class User:
      username: str               # Field
      email: str                  # Field
  ```

### **Kind 10: Enum**
- **Description**: Enumeration declarations
- **Usage**: Enum classes and enum values
- **Example**:
  ```python
  from enum import Enum
  
  class Status(Enum):             # Enum
      ACTIVE = 1
      INACTIVE = 2
  ```

### **Kind 11: Interface**
- **Description**: Interface declarations
- **Usage**: Abstract interfaces, protocols
- **Example**:
  ```python
  from typing import Protocol
  
  class Drawable(Protocol):       # Interface
      def draw(self) -> None: ...
  ```

## Practical Usage Examples

### Common Filter Combinations

#### Find All Callable Items
```python
include_kinds=[6, 12]  # Methods + Functions
```

#### Find Class Structure
```python
include_kinds=[5, 6, 9]  # Classes + Methods + Constructors
```

#### Find Data Definitions
```python
include_kinds=[13, 14]  # Variables + Constants
```

#### Exclude Imports and Modules
```python
exclude_kinds=[1, 2]  # Exclude Files + Modules
```

#### Find User-Defined Types
```python
include_kinds=[5, 10, 11]  # Classes + Enums + Interfaces
```

## Symbol Kind Usage in Flow-Bento Tools

### find_symbol Tool
```python
# Find all classes
find_symbol(name_path="User", include_kinds=[5])

# Find all methods in a class
find_symbol(name_path="User/*", include_kinds=[6], depth=1)

# Find constants only
find_symbol(name_path="MAX_*", include_kinds=[14], substring_matching=True)
```

### find_referencing_symbols Tool
```python
# Find method references, exclude imports
find_referencing_symbols(name_path="login", exclude_kinds=[2])

# Find class usage in methods only
find_referencing_symbols(name_path="User", include_kinds=[6])
```

## Language-Specific Considerations

### Python
- **Functions vs Methods**: Clear distinction between standalone functions (12) and class methods (6)
- **Properties**: Use `@property` decorator, classified as kind 7
- **Class Variables**: May be classified as variables (13) or constants (14) based on naming

### JavaScript/TypeScript
- **Functions**: Both function declarations and arrow functions are kind 12
- **Methods**: Class methods and object methods are kind 6
- **Interfaces**: TypeScript interfaces are kind 11

### Java/C#
- **Methods**: Instance and static methods are kind 6
- **Fields**: Instance and static fields are kind 8
- **Constructors**: Explicitly classified as kind 9

## Best Practices

### 1. Start Broad, Then Filter
```python
# First: Get overview
find_symbol(name_path="User")

# Then: Focus on specific types
find_symbol(name_path="User", include_kinds=[6])  # Methods only
```

### 2. Use Logical Combinations
```python
# Find all user-defined callable items
include_kinds=[6, 12]  # Methods + Functions

# Find all data storage items
include_kinds=[8, 13, 14]  # Fields + Variables + Constants
```

### 3. Exclude Noise
```python
# Skip imports when finding usage
exclude_kinds=[2]  # Exclude modules

# Skip files in detailed analysis
exclude_kinds=[1]  # Exclude file-level symbols
```

### 4. Context-Aware Filtering
```python
# API analysis: Focus on public methods
include_kinds=[6]  # Methods

# Configuration analysis: Focus on constants
include_kinds=[14]  # Constants

# Structure analysis: Focus on types
include_kinds=[5, 10, 11]  # Classes + Enums + Interfaces
```

## Troubleshooting

### Unexpected Results
- **Wrong kind classification**: Check if symbol is classified differently than expected
- **Missing symbols**: May be using wrong include_kinds filter
- **Too many results**: Add more specific exclude_kinds filters

### Language Server Differences
- Different language servers may classify symbols slightly differently
- Some symbols may have multiple classifications
- Dynamic symbols may not be captured

### Performance Considerations
- **Specific filtering**: Use include_kinds to reduce processing
- **Exclude common noise**: Use exclude_kinds=[1,2] to skip files/modules
- **Scope limitation**: Combine with relative_path for better performance

This reference enables precise symbol filtering and analysis across different programming languages and use cases.