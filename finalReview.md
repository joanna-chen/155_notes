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
