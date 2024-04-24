# Remote Input Management Library

The RIM Library includes an Android Service that runs on the robot to allow remote conrol over the device.

Following functionalities are offered:

1. Navigation
2. Interaction
3. App Management
4. Device Monitoring

> **_NOTE:_** Use the Remote Control App for easy remote control or for custom commands the Transfer Library!


## Installation

This requires you to use the Android Studio. For this follow these step to install the rimlibrary:

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

3. Include the rimlibrary into your project to be able to use it inside your apps build.gradle:
```
dependencies {
    implementation 'de.fhkiel.srcms.remote:rimlibrary:x.x.x'
}
```
Replace the x.x.x with the latest version of the RIM Library inside your Maven Repository.

> **_NOTE:_** There might be further implementations necessary (Server Sent Event Lib & Kotlin Serialization Lib)<br> `implementation 'com.github.heremaps:oksse:0.9.0'` & <br>`implementation 'org.jetbrains.kotlinx:kotlinx-serialization-json:1.6.3'`


## Class

### RemoteInputManagementService

Main service to subscribe to an server to receive data from an input. Service handles connection with subscribing and requesting timeout resets. Incoming data will be transferred to further processing steps.

#### _Functions_

**shutDown**

`shutDown()`

Shuts down the service and closes all connections to the server.

**startServiceForPepper**

`startServiceForPepper(srcmsRobot: SRCMSRobot, hostIp:String, apps: MutableList<SRCMSApp>)`

Starts a thread to run the receiver to open a connection to the server. Then sends a reset request for the timeout for the server connection every 5 seconds. <br>
Also sends basic information to server.

* Parameters:
	* `srcmsRobot`: The current robot object.
	* `hostIp`: The ip to connect to the remote server.
	* `apps`: All srcms apps located in the device.


#### _Companion Object_

**getService**

`getService()`

Returns the current service if bound.

* Return:
	* Instance of `RemoteInputManagementService`

**isBound**

`isBound()`

Returns whether an Android service is bound to the instance or not.

* Return:
	* `true` if an Android service is bound; `false` otherwise.

**setService**

`setService(service: RemoteInputManagementService)`

Sets the Android Service.

* Parameter:
	* `service`: Created RIM-Service that should be running on the device.



#### _Usage_

In order to start the RIM-Service, a `Service Connection` has to be established via an `Intent`. The service can then be set via a RIMBinder and `startServiceForPepper` can be called.

```
val connection = object : ServiceConnection {
    override fun onServiceConnected(name: ComponentName?, service: IBinder?) {
    	// Create RIMBinder
        val binder = service as RemoteInputManagementService.RIMBinder

        // Set service
        RemoteInputManagementService.setService(binder.getService())

       	// Start RIM Service for device Pepper
        RemoteInputManagementService.getService().startServiceForPepper(
            srcmsRobot,
            hostIp,
            apps
        )
        
    }

    override fun onServiceDisconnected(name: ComponentName?) {
    }
}

// Call Intent with RIM-Service
Intent(context, RemoteInputManagementService::class.java).let {
    context.bindService(it, connection, Context.BIND_AUTO_CREATE)
}
```

To shut the service down, get the service and call `shutDown()`.

`RemoteInputManagementService.getService().shutDown()`


### Input Handler

Handler for incoming data from server. 

#### _Functions_

**handle**

`handle(input: DCMessage)`

Handles json string from server sent event by converting data into data class and sends data body to fitting interpreter class.

* Parameters:
	* `input`: Valid Json string with an id and a body for further processing actions

#### Data classes

The following classes are holding data that can be interpreted by the RIM Service.

|Name|Data|
|---|---|
|DCAnimations| `resId: Int`,<br> `animation: String` |
|DCAudio| `audioValue: Int` |
|DCBuildAnimation| `animationRId: Int` |
|DCControlStick| `movementType: String`,<br> `speed: Float`, <br> `xValue: Float`,<br> `yValue: Float`, <br> `zValue: Float` |
|DCData| `typeData: JsonObject`,<br> `misc: DCMisc:` |
|DCInteraction| `speech: String?`,<br> `animation: Int:` |
|DCLaunchApp| `appPackage: String` |
|DCMessage| `meta: JsonObject, ` <br> `data: JsonObject` |
|DCMisc| `createdAt: Long` |
|DCSendAnimation| `animation: List<DCAnimations>` |
