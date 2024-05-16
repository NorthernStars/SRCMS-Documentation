# SRCMSAppIntent

The Social Robot CMS calls apps related to it via an explicit intent. It also sets some extras data for the intent which informs the called application about several data.

The `SRCMSAppIntent` class is part of the `de.fhkiel.srcms.lib` package and is used to manage the intent that a CMS (Content Management System) app was called with from the CMS. This class allows you to extract and store various data associated with the intent`.

## Class Details

### Properties

* `app`: `SRCMSApp?`: An instance of `SRCMSApp` representing the CMS app. It can be `null` if not provided.
* `data`: `JSONObject?`: A JSON object containing additional data associated with the intent. It can be `null` if not provided.
* `user`: `SRCMSUser?`: An instance of `SRCMSUser` representing the user associated with the intent. It can be `null` if not provided.
* `srcms`: `SRCMSData?`: An instance of `SRCMSData` representing SRCMS (Softbank Robotics Content Management System) data associated with the intent. It can be `null` if not provided.
* `robot`: `SRCMSRobot?`: An instance of `SRCMSRobot` representing a robot associated with the intent. It can be `null` if not provided.

### Methods

* `toExtrasBundle()`: `Bundle`: Converts the `SRCMSAppIntent` object to a `Bundle` containing the intent data. It returns the created `Bundle` object.

### Companion Object

The companion object contains utility methods for creating an instance of SRCMSAppIntent from an Intent.

* `INTENT_KEY_APP`: `String`: Constant representing the key for the app data in the intent.
* `INTENT_KEY_DATA`: `String`: Constant representing the key for the additional data in the intent.
* `INTENT_KEY_USER`: `String`: Constant representing the key for the user data in the intent.
* `INTENT_KEY_SRCMS`: `String`: Constant representing the key for the SRCMS data in the intent.
* `INTENT_KEY_ROBOT`: `String`: Constant representing the key for the robot data in the intent.
* `fromIntent(intent: Intent)`: `SRCMSAppIntent`: A static method that takes an `Intent` object and returns an instance of `SRCMSApp Intent` populated with the data from the intent.

## App Data (DEPRECATED)

key: <ins>_app_</ins> <br>
processing object: SRCMSApp

Information about the app, that is called with the intent.

|Key|Value|
|---|---|
|name| String: The name of the app inside the CMS (is normally the localized title) |
|revision| Number: Revision number  (normally increases with every release) |
|versionName| String: Human readable string version name |
|lastUpdated| Date when this app was last updated (or null) |
|packageString| The package String name of the application |


## Data

key: <ins>_data_</ins><br>
processing object: String > JSONObject

_Placeholder for future feature of saving JSON data for the logged in user. I not used at the moment._

## User

key: <ins>_user_</ins><br>
processing object: SRCMSUser

Information about the loggedin user (also see User Management):

|Key|Value|
|---|---|
|id | A Long value of the user id. It is identified using this id in the user database |
|name | Human readable name of the user |
| status | Status of the user |
| permissions | Permissions of the user |

## SRCMS Data

key: <ins>_srcms-data_</ins><br>
processing object: SRCMSData

Information about the configuration of the Social Robot CMS calling the intent.
This also includes infromation about the authenicated user and the robots global configuration.

|Key|Value|
|---|---|
|status| String: Current status of the SRCMS |
|showAppsCategory| String: Name of the category the SRCMS was showing, before the intent was called |
|preferences| JSON Object: SRCMS references, also including global robots preferences |


### Status

The SRCMS status of the SRCMS when calling the intent. Can be one of the following:

|Value|Description|
|---|---|
|NONE| Initial value, before anything happend.|
|ININTIATING| SRCMS is itiating its configuation and objets and loading available app.|
|INIT_FAILED| The initialization failed.|
|STARTING| SRCMS is starting and requesting for a valid user to login.|
|STARTED| The SRCMS started successfully.|
|START_FAILED| The SRCMS failed to start.|
|UPDATETING| The SRCMS is updateing some applications.|
|UPDATED| The SRCMS already called the update process duringthis session.|
|UPDATE_FAILED| The update process failed.|


### showAppCategory

A string representing th category package that was shown a the SRCMS calls the intent (see Applications). Normally this is the apps ctageory, that
recieves the intent.

### preferences

The SRCMS preferences as JSON object including information (key-value pais) about global preference value of the robot.

|Key|Value|
|---|---|
|pref_speech_speed| Number: Speed value of the robots speech in percent (50-400%, default is 100%)|
|pref_speech_pitch| Number: Pitch value to the robots speech in percent (50-200%, default is 100%)|
|pref_key_app_overview_big_buttons| Boolean: True if the SRCMS shows bigger buttons. Indicating to enable a design more usefull for visually disabled people.|
|pref_backstack_use| Boolean: True fi the SRCMS enabled the Android backstack for naviagtion . The app should also use this behaviour. The default value is false.|

For information about the robots speech tags see http://doc.aldebaran.com/2-5/naoqi/audio/altexttospeech-tuto.html#tag-tutorial

## Robot Data

key: <ins>_robot_</ins><br>
processing object: SRCMSRobot

Contains informations about the robot

|Key|Value|
|---|---|
|robot_name| Name of the robot.|
|_Additionally the object can contain several keys for each robot function. The value is always a JSON object containing an data the corresponding function needs. The SRCMSRobot object searches for any of the following keys and assigns the related function object itself (if available)._| - |
|default| Default robot functions not belonging to any robot part.|
|head |Robots head functions and head sensors.|
|speech| Robot speech and speech recognition.|
|body| Robots body functions and the tablet functions.|
|arms| The robots arms functions.|
|legs| The robots legs functions.|
|drive| The robots navigation functions.|

