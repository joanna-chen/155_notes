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
| abstract | N/A       | Contains at least one abstract method, no instantiation | N/A | N/A | implementation not defined, only signature and return type declared |
| final    | N/A       | Cannot be subclassed | N/A | Value cannot change | Cannot be overridden |
| static   | N/A       | N/A   | Not inner class | Exactly one instance for all objects | Exactly one instance for all objects |

  
### UML diagrams
  
* Basic class block
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

* UML Sequence diagrams
  * Gate: the starting point
    * fliled circle on the leftmost verge of the diagram
  * Instance: the objects involved in the sequence
    * can be thread, process, or system
    * box labelled with `{instance name}: {object type}`
  * Lifeline: vertical, dashed, unitless time line
    * creation and destruction of respective instances are drawn on the lifeline
  * Messages:
    * synchronous messages:
      * solid arrow head line labelled with the method call
      * drawn from the inquiring instance to the responding instance
      * inquiring instance is blocked and waits for the response
    * asynchronous messages:
      * response from a synchronous message
      * dotted arrow head line labelled with the field containing the response
      * the inquiring instance does **not** wait for the responding instance before continuing
    * message conditions
      * `[Guard] Action` format
      * condition to be met before the message can be issued
      
![](http://i.imgur.com/kxhug74.png)

## Multithreading analysis

### Why multithread?
  * Takes advantage of time when CPU would otherwise be idling
  * Allows programs to run in parallel with each other
  
### Threads and processes
  * Thread: a sequence of commands
    * faster to create and destroy than processes
    * threads within the same process have access to the same memory and files, and can communicate with each other
  * Process: a bunch of threads (at least one)
    * eg. An android app is a process that has a MainActivity thread and a UI Thread.
  * If any thread encounters an error, its entire process halts
  * Independent processes can continue if another one stops

### Thread Scheduling
  * **Threads have baggage**
    * required execution time
    * execution deadlines
    * required data (may come from other threads)
  * Threads have states:
    * Executing
    * Ready: all required data is ready, just waiting for a processor to occupy
    * Blocked: some needed resources are not yet ready
  * **Different Multithreading Strategies:**
    * Co-operative Multithreading
      * Each thread controls when it yields the CPU it occupies
      * Good for embedded systems that do not anage threads
      * Can be very efficient if every thread yields efficiently
      * Problem: **Greedy Threads** that never yield
    * Pre-emptive Multithreading
      * OS has the power to force threads to switch or yield CPU
      * Problem: if the OS's decisions are not efficient, then the system will have poor performance
  * Threads and deadlines
    * Hard deadlines: timely completion is extremely important
      * these tasks have higher priorities
    * Soft deadlines: occaisional delay is undesirable but tolerable
  * Race Conditions
    * Consider 2 seperate threads that act on the same data
    * If the threads are run at the same time, a race condition occurs
    * It's uncertain what the data will be after running the threads
    
## Software Testing
### Testing Levels:
  * **Smoke test:** adding code until it fails
  * **Unit test:** tests carried out on a small piece of code, testing only that piece of the software
    * **NO STATE DEPENDENCY**
    * can target algorithm bugs
  * **Integration test:** bringing multiple modules together and testing their combined behaviour
    * can target module incompatibility and heisenbugs
  * **System Test:** testing the entire system
    * can target unexpected system behavioural bugs
  * **Stress test**: testing software over an extended period of time with long, cyclic test plans
    * can target time-dependent bugs that wouldn't show up otherwise eg. memory leak
  * **Regression test:** testing that new updates to software do not break features that used to work
  
### JUnit stuff
  * assertEquals(String message, double expectedOutput, double actualOutput, double toleranceLevel)
  * `@Test` marks a test function
  * `@Test (expected = {exception class})` marks a test function that expects a thrown exception
  * `@Before` this function runs before every test function
  * `@After` `-_-`
  * `@BeforeClass` runs before the test class
  * `@AfterClass` used to dispose of the test class
  
### Test case design
  * Normal use cases
  * Edge/corner/boundary cases
  * Exception cases
  
### Coverage analysis
  * if a line of code is run in a test suite then its covered, otherwise not
  
## Debugging
### Types of bugs
  * Common bug
    * semantic mistake in code that causes 100% predictable (wrong) output
  * Sporadic bug
    * bug that only occurs under certain cases (normally boundary/edge conditions)
  * Heisenbug
    * very pain in the ass
    * difficult to isolate and happens inconsistently
    * commonly caused by race conditions, memory leaks, or optimization faults
    * if caused by simultaneous field access:
      * use **sychronize** to prevent variable conflicts
      * in the following example, the variable `s` is locked until execution finishes
```java
synchronized(s){
  s.count++;
  p.setResult(s);
}
```
      * make the field local instead of global/static whenever possible
  * Bugs hiding behind other bugs
    * multiple bugs interacting with each other
    * this happens when you try to implement too much code at once between testing
  * Secret bugs
    * you don't have access to the bug report due to some kind of reason
      * eg. company confidentiality or black box program
  * Configuration bug
    * an issue with the runtime environment instead of the actual code
    * eg. insufficient file access privelege
  * Hardware bug
    * not your problem
  * Not-a-bug
    * the program is doing something semantically correct based on the specifications
    * it's a problem for the project manager, not the programmer
### Debuggable coding style
  * don't make your code too clever
  * name variables in a useful way
  * comment with care
    * explain **purpose** clearly (not just what you're doing, but **why** you're doing it) and make sure outdated comments don't stay in code
    * or write code that is self-documenting
    
## Refactoring

### Property 1: Local - not affecting unrelated parts of program
### Property 2: Sematic-Preserving - code maintains identical behaviour

### General Refactoring Process
  1. Create Unit Test / Code Instrumentation
  2. Run Test
  3. Make Changes
  4. Run Test
  5. Evaluate Results
  
### Simple refactoring techniques
  * **Field/Method renaming:** rename fields and methods that have bad names
  * **Method extraction:** finding repeated sections of code and replacing them with a method call
  * **Magic numbers:** remove random numbers in code, replacing them with constants (fields declared final)
  
### OOD Refactoring Techniques
  * **Encapsulation:** making fields/methods private or public as necessary, hiding information from the rest of the program
  * **Generalizing Types:** making classes that have similar properties use inheritance instead of being seperate and bad
  * **Method/Class Extraction:** if a method/class behaves logically different in 2 different use cases, split it into a seperate method/class
  * **Inline Method/Class:** combining logically similar methods/classes into a single method/class
  * **Pull-up/Push-down:** moving methods from superclass to subclass or the other way around depending on how often they are used in each case
  * **Polymorphism:** replace conditions with polymorphism. pretty gud
  
### Antipatterns
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
