# Refactoring
Basic and OOD Techniques and Antipatterns

### Property 1: Local - not affecting unrelated parts of program
### Property 2: Sematic-Preserving - code maintains identical behaviour

## General Refactoring Process
1. Create Unit Test / Code Instrumentation
2. Run Test
3. Make Changes
4. Run Test
5. Evaluate Results

## Simple Refactoring Techniques
### Method Extraction:
   * Target: repeated segments of code
   1. extract repeated segments into standalone method
   2. replace all repeated segments with method call

### Magic Number Removal:
   * Target: random numbers with no meaning
   1. assign number to constant with meaningful name with ALL CAPS

### Field and Method Naming
   * Target: fields and methods with poor names
   1. Rename more descriptively; Longer names :: long-living fields, Shorter names :: temperory fields

## OOD Refactoring Techniques
### Encapsulated Fields:
   * Target: fields not suitable for public access
   1. Make fields `private` or `protected`
   2. Create getter-setter methods

### Generalizing Types:
   * Target: similar classes with repeated code
   1. Create superclass - concrete / abstract - and move repeated contents in
   2. Extend classes from superclass and implement code

### Extract Method / Class:
   * Target: Logically different code inside a method/class.
   1. Create new method / class
   2. Move logicall isolatable code into it.

### Inline Method / Class:
   * Target: Logically similar methods/classes should be integrated
   1. Combine the code from those instances into one
   
### Inline Method / Class UML Representation
![example UML refactoring](https://github.com/suzyng83209/155_notes/blob/master/uml%20refactoring.PNG)

### Move / Pull-up / Push-down
   * Target: fields and methods that logically belong elsewhere
   1. Pull-up: repeated use in subclasses; move to superclass
   2. Push-Down: rarely used in superclass; move to subclass
![uml pull up](https://github.com/suzyng83209/155_notes/blob/master/uml%20pull-up.PNG)

## Antipattern:
Code stye that promotes mistakes

1. The Blob
   * Too much logic in one class; keeps expanding.
   * Should extract methods
   
2. Lava Flow
   * old code segments that may or may not break the program if removed carelessly
   * code review and maintenance and deletion
   
3. Functional Decomposition
   * coding style resembles sequential languages when OOP (when non-OOD programmers write in OOD languages)
   * Exctract and pull-up
   
4. Copy-and-Paste
   * repeated code that is slightly modified
   * extract to own method and replace copied segments
   
5. Poltergeists
   * class with limited roles and short lifecycle - Waste of system resources
   * inline methods / class
   
6. Golden Hammer
   * Class designed to handle every possible event in program
   * extract and specialize classes
   
7. Expections as Control Flow
   * using try-catch block to handle expected Exceptions
      ```java
      try {
        instance1.method();
      } catch (NullPointerException) {
        System.out.println("instance is empty");
      }
      ```
   * replace with if-else
      ```java
      if (instance1 != null {
        instance1.method();
      } else {
         System.out.println("instance is empty");
      }
      ```
8. Spaghetti Code
   * code with no structure suh as small number of objects with long methods
   * extract methods and restructure

