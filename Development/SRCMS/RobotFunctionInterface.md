# RobotFunctionInterface

The RobotFunctionInterface is an abstract interface representing aframework for building robot functions.
It provides a set of methods and properties to manage the lifecycle and functionality of robot functions. This interface extends the RobotLifecycle Callbacks interface from the QiSDK (Softbank Robotics SDK) to handle robot focus events.

## Properties

* `function`: A property of type `FUNCTIONS` representing the specific function type of the robot function.
* `TAG`: A property of type `String` representing the tag used for logging purposes.
* `qiContext`: A mutable property of type `QiContext?` representing the `QiContext` object associated with the robot function.

## Methods

#### updateQiContext

`fun updateQiContext(qiContext: QiContext?): QiContext?`

A method used to update the QiContext object associated with the robot function. It takes a `QiContext` parameter and returns the updated `QiContext` object.

### Overridden Methods

The RobotFunctionInterface implements the following overrides from the RobotLifecycleCallbacks interface:

#### onRobotFocusGained

`fun onRobotFocusGained(qiContext: QiContext?)`

This method is called when the robot gains focus. It updates the QiContext object and logs the event.

#### onRobotFocusLost

`fun onRobotFocusLost()`

This method is called when the robot loses focus. It updates the QiContext object to null and logs the event.

#### onRobotFocusRefused

`fun onRobotFocusRefused(reason: String?)` 

This method is called when the robot focus is refused. It logs the event along with the reason for the refusal.

## Companion Object

The RobotFunctionInterface includes a companion object that provides additional constants:

* `JSON_NAME`: A constant `String` representing the key name for the name property when serializing to JSON.


## Enumerations

The `FUNCTIONS` enumeration represents the available function types for the robot function. Each enum value includes a key representing the function
type and an optional classType that corresponds to the specific class implementation for that function type.

Please note that this interface is meant to be implemented by concrete robot function classes to define specific functionality for different robot
functions.

