# Exam structure: 5 major questions

## 1: Multiple Choice
* Code analysis
* testing
* debugging
* OOD
* UML
* Licensing (!)

## 2: Advanced FSM design
* UML diagrams
* Code implementation

## 3: Event Driven Programming, OOD
* Timer analysis
* Android development
* Parametric Polymorphism

## 4: Multithreading
* Thread scheduling
* UML sequence diagram analysis

## 5: Testing and Refactoring
* Whitebox testing
* Code coverage
* JUnit suite implementation
* Code refactoring

# Concept Reviews

## Event-driven programming

* Event-Handler Relationship:
  * sensor > event manager > handler > actuator
  * Inversion of control: the system/users/environments decides what happens, not the program

* Polling vs interrupt
  * Polling: periodically watches a parameter
  * Interrupt: raises attention when parameter is confirmed to be changed

* Try-Catch-Finally block
  * Executes the code that comes after the try block
  * If an exception is thrown, handle it in the Catch block
  * Finally block always runs after everything is finished
  * Don't use this for control flow

## Android development

* Android application structure

* **activity**: full-screen window that users can interact with
* **widgets (views)**: interactive items that allow for user interactions
* **task (activity call stack)**: android OS has a task stack (prevents disruption to functional dependency)

* Bundle
  * Bundle is a key-value map used to restore information when the app is closed/inactive
  * onSaveInstanceState is called in onDestroy() right before the activity is destroyed
  * This code saves "blue" to the key "color"
```java
class MainActivity ... {

 @Override
 protected void onSaveInstanceState(Bundle b) {
  super.onSaveInstanceState(b);
  b.putString("color", "blue");
 }
}
```
  * This code gets the stored data from the bundle when the activity is created
```java
protected void onCreate(Bundle b) {
  if (b != null) {
    data = b.getString("color");
  }
}
```

## Timers

### How they work
* When you schedule a TimerTask, the TimerTask is the event handler for a TimerElapsed event that procs after the timeout you set
* Scheduled timers run in parallel with other timers and the main method
* Watchdog timer
 * Timer that is used to make sure a task that can potentially timeout (fetching something from the internet, connecting to another device wirelessly, etc) doesn't continue retrying forever and stall out the system
 
### Timer Coalescing
 * In a system without timer coalescing, timeouts fire at pretty evenly distributed times
 ![neener neener](https://cdn.arstechnica.net/wp-content/uploads/2013/06/coalesced_before.png)
 * This means that the CPU has to constantly be using power, leading to lots of idle time or generally inefficient CPU use
 * Timer coalescing groups up and timeout events that are close to each other, meaning that the CPU works in short bursts of high activity instead of constant light use
 ![neener neeeeener](https://cdn.arstechnica.net/wp-content/uploads/2013/06/coalesced-after.png)
 * Good for power efficiency
 
## OOD design

### Class Comparison
|        | Concrete Class | Abstract Class      | Interface                        |
|:-------|:---------------|:--------------------|:---------------------------------|
| Fields | No restriction | Public or protected | Public default, Constant default |
| Methods| must be implemented | unimplemented are abstract | signature only |
| Declaration | `class` | `abstract class` | `interface` |
|Instantiability| Y | N | N |
|Inheritance | extends | extends | implements |
|multiple inheritance| N | N | Y |
|other | has constructors and destructors | can contain all concrete methods; no constructor | no scpoe modifier; uniqueness modifier required|

### Modifiers
| Modifier | Interface | Class | Nested Class | Field | Method |
|:---------|-----------|-------|--------------|-------|--------|
| public   | Accessible from any class                         |
| private  | Accessible only from the `this`                   |
| protected| Accessible from within package (`this` and subclasses) |
| none     | Accessible from any class within same package (BAD)|
| abstract | N/A       | Contains at least one abstract method, no instantiation | N/A | implementation not defined, only signature and return type declared |
| final    | N/A       | Cannot be subclassed | Value cannot change | Cannot be overridden |
| static   | N/A       | N/A   | Not inner class | Exactly one instance for all objects | Exactly one instance for all objects |

  
### UML diagrams
  
* basic class block
  * 3 rows:
    1. class name (bold)
    2. attributes/fields : data type
    3. operations (constructors, methods, etc) : return type
  * visibility modifier (put in front of field/method): public (+), private (-), protected (#)
  * uniqueness modifier: static (underline), final (capitalization)
  * destructor/package (~)
  * range of values (..)
  * separator of items in set (,)
  * *in* in front of input parameters
  * *out* in front of output parameters
