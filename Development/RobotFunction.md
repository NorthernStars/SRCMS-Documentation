# RobotFunction

The RobotFunction class is a part of the `de.fhkiel.srcms.lib.robot` package and serves as a base class for defining specific robot functions. It implements the `RobotFunctionInterface` and provides methods for managing values associated with the function.

## Constructors

`RobotFunction(function: RobotFunctionInterface.FUNCTIONS)`

Creates an instance of the `RobotFunction` class.

* Parameters:
	* `function`: [RobotFunctionInterface.FUNCTIONS] - The enumeration value representing the specific robot function.


## Properties

* `function: RobotFunctionInterface.FUNCTIONS`
 	* The enumeration value representing the specific robot function.
* `TAG: String`
	* A string representing the tag of the class.
* `qiContext: QiContext?`
	* The `QiContext` for accessing the QiSDK for the Pepper robot from Softbank Robotics. <br>It is initially set to `null`.


## Methods

#### equals

`fun equals(other: Any?): Boolean`

Overrides the `equals` method to compare two `RobotFunction` objects.

* Parameters:
	* `other`: [Any] - The object to compare with.
* Returns: 
	* `Boolean` - `true` if the objects are equal, `false` otherwise.

#### getValues

`fun getValues(valuesToFilter: List<String>? = null): Map<String, Any?>`

Retrieves the values from the internal values map associated with this function.

* Parameters:
	* `valuesToFilter`: [List&lt;String>, optional] - A list of keys to filter the values. <br>If `null` (default), the complete map of values is returned.
* Returns: 
	* `Map<String, Any?>` - The values associated with this function.

#### getValue

`fun getValue<T>(valueName: String): T?`

Retrieves a specific value of type `T` from the values associated with this function.

* Parameters:
	* `valueName`: [String] - The name of the value to retrieve.
* Returns: 
	* `T` - The value of type `T`, or `null` if not found.

#### setValues

`fun setValues(vararg values: Pair<String, Any?>): Map<String, Any?>`

Sets one or more values to this function.

* Parameters:
	* `values`: [vararg Pair<String, Any?>] - The key-value pairs to set. The first element of each pair is the key, and the second element is the value of type Boolean, Int, Double, Long, String, JSONObject, or JSONArray.
* Returns:
	* `Map<String, Any?>` - The updated map of internal values.


#### setValues

`fun setValues(json: JSONObject): Map<String, Any?>`

Sets the values of this function to the internal map using the JSON keys.

* Parameters:
	* `json`: [JSONObject] - The JSON object containing the data to set as internal values.
* Returns: 
	* `Map<String, Any?>` - The updated map of internal values.


#### toJSON

`fun toJSON(): JSONObject` 

Converts the function to a `JSONObject` representation.

* Returns: 
	* `JSONObject` - The `JSON` object representing the function.


#### hashCode

`fun hashCode(): Int` 

Overrides the `hashCode` method to generate a hash code for the `RobotFunction` object.

* Returns: 
	* `Int` - The generated hash code.

## Companion Object

#### functionsMap

`fun functionsMap: Map<String, RobotFunctionInterface.FUNCTIONS>`

A map that generates the relationship between a string value (such as in JSON) and the corresponding RobotFunctionInterface.FUNCTIONS enumeration value.

#### getFunction

`getFunction<T: RobotFunction>(functionName: String): T?`


## Usage

```
import org.json.JSONObject

fun main() {
    // Create a new RobotFunction instance
    val robotFunction = RobotFunction(RobotFunctionInterface.FUNCTIONS.SPEECH)
    
    // Set values for the robot function
    robotFunction.setValues("volume" to 50, "pitch" to 1.5)

    // Get a specific value from the robot function
    val volume = robotFunction.getValue<Int>("volume")
    println("Volume: $volume")

    // Generate a JSON representation of the robot function
    val json = robotFunction.toJSON()
    println("JSON representation:")
    println(json.toString())

    // Create a new robot function from a JSON object
    val jsonString = "{\"volume\":80, \"pitch\":2.0}"
    val newFunction = RobotFunction(RobotFunctionInterface.FUNCTIONS.SPEECH)
    newFunction.setValues(JSONObject(jsonString))

    val newVolume = newFunction.getValue<Int>("volume")
    val newPitch = newFunction.getValue<Double>("pitch")
    
    println("New Volume: $newVolume")
    println("New Pitch: $newPitch")
}
```

We create a new instance of `RobotFunction` with the `RobotFunctionInterface.FUNCTIONS.SPEECH` enumeration value. 

We set the values for the speech function, specifying the "volume" and "pitch" key-value pairs using the `setValues` method.

Next, we retrieve the value of the "volume" from the robot function using the `getValue` method and print it to the console.

We then generate a JSON representation of the robot function using the `toJSON` method and print it to the console.

Afterward, we simulate creating a new `RobotFunction` object from a JSON string representation. We set its values using the `setValues` method with a `JSONObject`. We extract the "volume" and "pitch" values from the new function using the `getValue` method and print them to the console.

Please note that you should have the necessary dependencies and implementations in place for the code to compile and run successfully.