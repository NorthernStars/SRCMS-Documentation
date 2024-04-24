# Transfer Library

The Transfer Library is the interface between a data emitter, the server, and the data receiver (most probably: Remote Input Management Library). It offers all the necessary functions to transfer data, in the form of `JSON` objects, to the server (server will process data and send it accordinly to the corresponding endpoint). The Transfer Library provides the option of creating an emitter or a receiver to communicate with the server.

The Transfer Library consist of the following main classes/objects:

* SRCMSEmitter
* SRCMSEmitterJSONBuilder
* SRCMSReceiver
* SRCMSReceiverJSONBuilder
* Utils

Enum classes will help with consistent naming. The following exist:

* Descriptor
* DeviceType
* MovementType
* Type


## Installation

This requires you to use the Android Studio. For this follow these step to install the transferlib:

1. Clone the git maven repository from https://bitbucket.iue.fh-kiel.de/projects/SRC/repos/srcms-lib-maven/ to your local maven repository
location:

	a. Windows: `C:\Users\<username>\.m2`<br>
	b. Linux: `/home/<username>/.m2`<br>
	c. Mac: `/Users/<username>/.m2`

> **_NOTE:_** The git repository content must be copied into a sub-directory named repository!

2. Include the maven local repository:<br>
Add the mavenlocal() to your projects settings.gradle:
```
pluginManagement {
	repositories {
		mavenLocal()
	}
}
```

3. Include the transferlib into your project to be able to use it inside your apps build.gradle:
```
dependencies {
    implementation 'de.fhkiel.srcms.remote:transferlib:x.x.x'
}
```
Replace the x.x.x with the latest version of the Transfer Library inside your Maven Repository.

> **_NOTE:_** There might be further implementations necessary (Server Sent Event Lib)<br> `implementation 'com.github.heremaps:oksse:0.9.0'`


## Classes

Each of the main class (`SRCMSEmitter` & `SRCMSReceiver`) owns a corresponding Json builder class (`SRCMSEmitterJSONBuilder` & `SRCMSReceiverJSONBuilder`) to ensure proper `JSON` objects.

### SRCMSEmitter

The emitter reflects an application or device aiming to communicate with the robot. For an emitter to be created, it must know the robots name it wants
to connect to. It will get a list of all registered robots from the server and can choose the right robot from the list. A successfully created emitter has several methods to choose from.

#### _Constructor_

`SRCMSEmitter(robotName: String)`

Creates a emitter for the robot with the corresponding name.

#### _Functions_


**buildAnimation**

`buildAnimation(sessionUUId: UUID, animationResourceId: Int)`

Sends an build animation command on the server associated with the specified session UUID and animation resource ID.

* Params:
	* `sessionUUId`: The unique identifier of the server session during which the animation is being built.
    * `animationResourceId`: The resource ID of the animation to be built.
* Returns:
	* An HTTP status code as an `Int`, reflecting the outcome of the emission. Successful emissions will return the status code `200`, and failures will return `500`.


**closeSession**

`closeSession(sessionUUId: UUID)`

Closes the session associated with the specified session UUID on the server.

* Params:
	* `sessionUUId`: The UUID of the session to be closed.
* Returns:
	* An HTTP status code as an `Int`, reflecting the outcome of the emission. Successful emissions will return the status code `200`, and failures will return `500`.

**emitAnimationData**

`emitAnimationData(sessionUUId: UUID, animation: Int)`

Emits a new animation command for the robot.

* Params:
	* `sessionUUId`: The unique identifier of the server session during which the animation data is being sent.
     * `animation`: Resource id of the animation.
* Returns:
	* An HTTP status code as an `Int`, reflecting the outcome of the emission. Successful emissions will return the status code `200`, and failures will return `500`.



**emitAudioData**

`emitAudioData(sessionUUId: UUID, newAudioValue: Int)`

Sends audio data to a connected server using a specified session UUID and audio value.

* Params:
	* `sessionUUId`: The unique identifier of the server session during which the audio data is being sent.
    * `newAudioValue`: The new audio value to be transmitted.
* Returns:
	* An HTTP status code as an `Int`, reflecting the outcome of the emission. Successful emissions will return the status code `200`, and failures will return `500`.
    

**emitControllerData**

```
emitControllerData(
        sessionUUId: UUID,
        type: MovementType, 
        speed: Float, 
        valueX: Float, 
        valueY: Float, 
        valueZ: Float
    )
```

Emits a new controller movement action.

* Params:
	* `sessionUUId`: The unique identifier of the server session during which the controller data is being sent.
	* `type`: of the controller motion.
    * `speed`: Speed as a `Float` value.
    * `valueX`: Value of the new X coordinate.
    * `valueY`: Value of the new Y coordinate.
    * `valueZ`: Value of the new Z coordinate.
* Returns:
	* An HTTP status code as an `Int`, reflecting the outcome of the emission. Successful emissions will return the status code `200`, and failures will return `500`.
    

**emitInteractionData**

`emitInteractionData(sessionUUId: UUID, text: String, animation: Int)`

Emits a new animation command for the robot.

* Params:
	* `sessionUUId`: The unique identifier of the server session during which the interaction data is being sent.
    * `text`: Text to be transmitted.
    * `animation`: Resource id of the animation.
* Returns:
	* An HTTP status code as an `Int`, reflecting the outcome of the emission. Successful emissions will return the status code `200`, and failures will return `500`.


**emitLaunchAppData**

`emitLaunchAppData(sessionUUId: UUID, appPackage: String)`

Sends a launch app command to the server using the specified session UUID and app package name.

* Params:
	* `sessionUUId`: The unique identifier of the session during which the app launch command is being sent.
    * `appPackage`: The package name of the app to be launched.
* Returns:
	* An HTTP status code as an `Int`, reflecting the outcome of the emission. Successful emissions will return the status code `200`, and failures will return `500`.


**emitSpeechData**

`emitSpeechData(sessionUUId: UUID, text: String)`

Emits a new speech command for the robot.

* Params:
	* `sessionUUId`: The unique identifier of the server session during which the speech data is being sent.
     * `text`: Text to say.
* Returns:
	* An HTTP status code as an `Int`, reflecting the outcome of the emission. Successful emissions will return the status code `200`, and failures will return `500`.


**getAnimation**

`getAnimation(sessionUUId: UUID)`

Retrieves animation data associated with the specified session UUID from the server.

* Params:
	* `sessionUUId` The UUID of the server session for which to retrieve animation data.
* Returns:
	* A `map` containing animation `resource ids` as keys and corresponding `Boolean` values indicating whether each animation is built (`true`) or not (`false`). If an error occurs or the animation data is not found, an `empty` map is returned.


**getInAction**

`getInAction()`

Gets a status if the robot is busy.

* Returns:
	* `Int` value of `-1` if robot is not busy.


**getRobotBaselineData**

`getRobotBaselineData()`

Gets the baseline information from a specific robot.

* Returns:
	* `JSONObject` with robots data


**getSession**

`getSession(appUUId: UUID)`

Retrieves the session UUID associated with the specified application UUID from the server.

* Params:
	* `appUUId` The UUID of the application for which to retrieve the session UUID.
* Retruns:
	* The session UUID as a `UUID` object if retrieved successfully; `null` otherwise


**openSession**

`openSession(appUUId: UUID)`

Initiates a session with the server using the specified application UUID.

* Params:
	* `appUUId` The UUID of the application for which to open a session.
* Returns:
	* An HTTP status code as an `Int`, reflecting the outcome of the emission. Successful emissions will return the status code `200`, and failures will return `500`.


**sendAnimation**

`sendAnimation(sessionUUId: UUID, animationMap: Map<Int, String>)`

Sends animation data (whole animations for the robot to play) to the server using the specified session UUID and animation map.

* Params:
	* `sessionUUId`: The unique identifier of the server session during which the animation data is being sent.
     * `animationMap`: A map where each key is an `Int` representing the resource ID of the animation, and each value is a `String` representing the animation data.
* Returns:
	* An HTTP status code as an `Int`, reflecting the outcome of the emission. Successful emissions will return the status code `200`, and failures will return `500`.



#### _Companion Object_

**getRobotDevices**

```
getRobotDevices(
            rwsDomainIpv4Address: String,
            portNumber: Int
        )
```

Retrieves information about available robot devices from the server.

* Params:
	* `rwsDomainIpv4Address`: The IPv4 address of the RWS domain.
    * `portNumber`: The port number on which the RWS domain is running.
* Returns:
    * A `mutable list` of pairs, where each pair consists of a robot name and its corresponding IP address.

#### _Usage_

```
// Server config
val rwsIp = "192.168.0.1"
val rwsPort = 9337

var emitter: SRCMSEmitter? = null
var robots: MutableList<Pair<String, String>? = null

// Get registered robots
SRCMSEmitter.getRobotDevices(rwsIp, rwsPort).let { robotPairs ->
    robots = it
}

// Select robot name from list
emitter = SRCMSEmitter(robots[0].first)

// Create an appUUID for a session
val appUUID = UUID.randomUUID()

// Open session and get session
emitter?.openSession(appUUID)
val sessionUUID = emitter?.getSession(appUUID)

// Transmit data
emitter?.emitInteractionData(sessionUUID, text, animationId)

// Close session 
emitter?.closeSession(sessionUUID)
```

### SRCMSReceiver

Using the receiver, a connection to the server is created and maintained continuously via a HTTP-GET request, the `resetTimeOut()` method. To create a receiver, you need the robot name, the device type, as well as the server IP address, and its port. The core task of the receiver is the registration and subscription of the device to the server, as well as the processing of the incoming data.

#### _Constructor_

`SRCMSReceiver(deviceName: String, deviceType: DeviceType, rwsIp: String, rwsPort: Int)`

Creates a node to the Remote Webservice Server to receive data send to the RWS by an emitter.

#### _Functions_

**close**

`close()`

Closes the connection.

**getActiveSessions**

`getActiveSessions()`

Retrieves active session UUIDs from the server.

* Returns:
	* A `list` of `UUID` representing the active sessions


**register**

`register()`

Registers a robot to the Remote Webservice Server.

* Returns:
	* An HTTP status code as an `Int`, reflecting the outcome of the emission. Successful emissions will return the status code `200`, and failures will return `500`.


**resetTimeout**

`resetTimeOut()`

Notifies Remote Webservice Server not to close connection chanel.

* Returns:
	* An HTTP status code as an `Int`, reflecting the outcome of the emission. Successful emissions will return the status code `200`, and failures will return `500`.


**sendRobotBaselineData**

`sendRobotBaselineData(data: JSONObject)`

Sends baseline information to the Remote Webservice Server.

* Params:
	* `data`: `JSONObject` of all the data. To ensure a valid JSONObject use `SRCMSReceiverJSONBuilder` with the fitting function depending on your robot device.
* Returns:
	* An HTTP status code as an `Int`, reflecting the outcome of the emission. Successful emissions will return the status code `200`, and failures will return `500`.


**setAnimationList**

`setAnimationList(sessionUUId: UUID, savedAnimation: Map<Int, Boolean>)`

Sets the animation list associated with the specified session UUID on the server.

* Params:
	* `sessionUUId`: The `UUID` of the server session for which to set the animation list.
    * `savedAnimation`: A `map` containing animation resource IDs as keys and boolean values indicating whether each animation is built (`true`) or not (`false`).
* Returns:
	* An HTTP status code as an `Int`, reflecting the outcome of the emission. Successful emissions will return the status code `200`, and failures will return `500`.



**setInAction**

`setInAction(inAction: Int)`

Set whether the robot is currently busy doing action.

* Params:
	* `inAction`: `Int` whether robot is interacting (`-1` = not in action)
* Returns:
	* An HTTP status code as an `Int`, reflecting the outcome of the emission. Successful emissions will return the status code `200`, and failures will return `500`.



**subscribe**

`subscribe(listener: Listener)`

Subscribes the robot to the Remote Webservice Server.

* Params:
	* `listener`: `Listener` interface with several functions to handle information from the Server.
* Returns:
   	* `ServerSentEvent` chanel to receive data transmitted by the Server.
   

#### _Usage_

```
// Server configuration
val rwsIP = "192.168.0.1"
val rwsPort = 9337

var srcmsReceiver: SRCMSReceiver? = null

// Creates the receiver
srcmsReceiver = SRCMSReceiver("Pepper", DeviceType.PEPPER, rwsIp, rwsPort)

// Register and subsrcribe to server
srcmsReceiver.register() 

srcmsReceiver.subscribe(object : Listener {
	override fun onOpen(sse: ServerSentEvent?, response: Response?) {}

	override fun onMessage(sse: ServerSentEvent?, id: String?, event: String?, message: String?) {
	    // Handle incoming data
	}

	override fun onComment(sse: ServerSentEvent?, comment: String?) {}

	override fun onRetryTime(sse: ServerSentEvent?, milliseconds: Long): Boolean {
	    return false
	}

	override fun onRetryError(sse: ServerSentEvent?, throwable: Throwable?, response: Response?): Boolean {
	    return false
	}

	override fun onClosed(sse: ServerSentEvent?) {}

	override fun onPreRetry(sse: ServerSentEvent?, originalRequest: Request?): Request? {
	    return originalRequest
	}
})

// Reset timeout to prevent server closing the connection
srcmsReceiver.resetTimeOut()

// Sending baseline information
srcmsReceiver.sendRobotBaselineData(SRCMSReceiverJSONBuilder("Pepper")
	.buildPepperBaselineJson(
	    batteryStatus = 50,
	    chargingFlap = true,
	    volumeLevel = 100,
	    pitch = 100,
	    speed = 100,
	    appMap = mapOf("app_one" to "com.example.app_one", "app_two" to "com.example.app_two")
	)
)

// Close connection
srcmsReceiver.close()
```

### SRCMSReceiverJSONBuilder

#### _Functions_

**buildPepperBaselineJson**

```
buildPepperBaselineJson(
        batteryStatus: Int,
        chargingFlap: Boolean,
        volumeLevel: Int,
        pitch: Int,
        speed: Int,
        appMap: Map<String, String>
    )
```

Builds a baseline `JSONObject` for Pepper. Baseline includes status information as well as existing apps and animations.

* Parameters:
	* `batteryStatus`: Battery status of Pepper.
    * `chargingFlap`: State of Peppers charging flap.
    * `volumeLevel`: Robots tablet volume.
    * `pitch`: Robots voice pitch.
    * `speed`: Robots voice speed.
    * `appMap`: Map of apps. `String` name of app and `String` the package name.
* Returns:
    * Interpretable `JSONObject` by the RWS.


## Enums


| Name | Constants | Description |
| --- | --- | --- |
| DeviceType | `Pepper("Pepper")` <br> `TEMI("Temi")` <br> `OTHER("Other")`| Enum of robots and devices |
| Descriptor |  `RECEIVER("Receiver")` <br> `EMITTER("Emitter")`| Enum of descriptors |
| MovementType | `LINE("Line")`<br> `ROTATION("Rotation")`<br> `DIAGONAL("Diagonal")`<br> `STOP("Stop")` | Enum of different motion types for the robot |
| Type | `CONTROLSTICK("ControlStick"`)<br> `INTERACTION("Interaction")`<br> `AUDIO("Audio")`<br> `BASELINE("Baseline")`<br> `SEND_ANIMATION("SendAnimation")`<br>`BUILD_ANIMATION("BuildAnimation")` <br> `LAUNCH_APP("LaunchApp")` <br> `UNSPECIFIED("Unspecified")` | Enum of valid data types for the remote service |
