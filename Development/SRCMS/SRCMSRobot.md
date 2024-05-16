# SRCMSRobot

The SRCMSRobot class is a part of the `de.fhkiel.srcms.lib.robot` package and is responsible for handling robot functions and communication with the robot's SDK. It provides a set of predefined robot functions and allows for generating and parsing JSON representations of robot data.

## Constructors

```
SRCMSRobot(
	name: String = ROBOT_NAME_DEFAULT, 
	robotFunctions:`HashMap<RobotFunctionInterface.FUNCTIONS, RobotFunction>, 
	qiContext: QiContext? = null
)
```

* Creates an instance of the `SRCMSRobot` class.

* Parameters:
	* `name`: [String, optional] - Name of the robot. Defaults to "Pepper" if not provided.
	* `robotFunctions`: [HashMap &lt;RobotFunctionInterface.FUNCTIONS, RobotFunction>] - A map of available robot functions. The map should contain instances of `RobotFunction` implementations for each desired robot function.
	* `qiContext`: [QiContext, optional] - QiContext for accessing the QiSDK for the Pepper robot from Softbank Robotics. Default is null.

## Properties

* `name: String`
	* The name of the robot.
* `robotFunctions: HashMap<RobotFunctionInterface.FUNCTIONS, RobotFunction>`
	* A map of available robot functions.
	* Key: [RobotFunctionInterface.FUNCTIONS] - An enumeration representing the available robot functions.
	* Value: [RobotFunction] - An instance of a `RobotFunction` implementation representing a specific robot function.
* `qiContext: QiContext?`
	* The QiContext for accessing the QiSDK for the Pepper robot from Softbank Robotics. <br>It is initially set to null and should be updated when the robot focus is gained.

## Methods

#### toJSON

`fun toJSON(): JSONObject`

Generates a `JSONObject` containing the data of the `SRCMSRobot` object.

* Returns: 
	* `JSONObject` - The generated `JSONObject`.

### Overridden Methods

#### onRobotFocusGained

`onRobotFocusGained(qiContext: QiContext?)`

Called when the robot focus is gained.

* Parameters:
	* `qiContext`: [QiContext] - The QiContext obtained for the robot.

#### onRobotFocusLost

`onRobotFocusLost()`

Called when the robot focus is lost.

#### onRobotFocusRefused

`onRobotFocusRefused(reason: String?)`

Called when the robot focus is refused.

* Parameters:
	* `reason`: [String] - The reason for the refusal.

## Companion Object

The companion object contains utility methods for working with `SRCMSRobot` objects.

#### fromJSON

`fromJSON(string: String): SRCMSRobot`

Parses a JSON string representation of a `SRCMSRobot` object and creates a corresponding instance of the `SRCMSRobot` class.

* Parameters:
	* `string`: [String] - The JSON string representation of a `SRCMSRobot` object.
* Returns: 
	* `SRCMSRobot` - The created `SRCMSRobot` object.


#### fromJSON

`fromJSON(jsonData: JSONObject): SRCMSRobot`

Converts a `JSONObject` representation of SRCMS config into a `SRCMSRobot` object.<br> Uses default values if no matching keys are found inside the `JSONObject`.

* Parameters:
	* `jsonData`: [JSONObject] - The preference data containing the robot information.
* Returns: 
	* `SRCMSRobot` - The created `SRCMSRobot` object.


## Usage

```
import org.json.JSONObject

fun main() {
    //Create a new SRCMSRobot instance
    val robot = SRCMSRobot("MyRobot")

    // Access and modify robot properties
    println("Robot name: ${robot.name}")
	robot.name = "NewRobotName"
    println("Modified robot name: ${robot.name}")
    
    // Add a new robot function
    val newFunction = CustomRobotFunction()
    robot.robotFunctions[RobotFunctionInterface.FUNCTIONS.CUSTOM] = newFunction
    
    // Generate a JSON representation of the SRCMSRobot object
    val json = robot.toJSON()
    println("JSON representation:")
    println(json.toString())
	
	// Parse a JSON string and create a SRCMSRobot object
    val jsonString = "{\"robot_name\":\"AnotherRobot\",\"SPEECH\":{\"volume\":50}}"
    val newRobot = SRCMSRobot.fromJSON(jsonString)
    println("Parsed robot name: ${newRobot.name}")
    println("Parsed robot functions:")
    
    newRobot.robotFunctions.forEach {(functionType, function) ->
        println("${functionType.name}: ${function.javaClass.simpleName}")
    }
}
```