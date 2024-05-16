# SRCMSApp

The SRCMSApp class is designed to represent an app available inside the Content Management System (CMS). It provides information about the app, such as its name, launch intent, icon, revision, version name, last updated date, description, and package information. The class also includes methods for retrieving the package name and launch intent of the app.

## Constructors

The `SRCMSApp` class has a primary constructor with the following parameters:

* `name` (String): The name of the app.
* `launchIntent` (Intent?): The launch intent of the app.
* `icon` (Drawable?): The icon of the app.

## Properties

The SRCMSApp class has the following properties:

* `revision` (Long): The revision number of the app.
* `versionName` (String): The version name of the app.
* `lastUpdated` (Date?): The last updated date of the app.
* `description` (String?): The description of the app.
* `packageString` (String?): The package name of the app.

## Methods

The `SRCMSApp` class provides the following methods:

#### getPackageName

`fun getPackageName(): String?`

This method returns the package name of the app. If the launch intent is available, it retrieves the
package name from the intent. Otherwise, it returns the package name stored in the packageString
property.

* Parameters: None.
* Returns:
	* `String?`: The package name of the app if available, otherwise `null`.

#### getLaunchIntent

`fun getLaunchIntent(packageManager: PackageManager): Intent?`

This method retrieves the launch intent of the app. If the launch intent is available, it returns the intent.
Otherwise, it uses the package manager to retrieve the launch intent based on the package name stored in the `packageString` property.

* Parameters:
	* `packageManager` (PackageManager): The package manager instance used to retrieve the launch intent.
* Returns:
	* `Intent?`: The launch intent of the app if available, otherwise null.

#### toJSON

`fun toJSON(): JSONObject`

This method converts the `SRCMSApp` object to a JSON object.

* Parameters: None.
* Returns:
	* `JSONObject`: The JSON object representing the `SRCMSApp` object

## Companion Object

The `SRCMSApp` class includes a companion object with the following methods:

#### fromJSON

`fun fromJSON(string: String): SRCMSApp?`

This method creates an `SRCMSApp` object from a JSON string.

* Parameters:
	* `string` (String): The JSON string representing the `SRCMSApp` object.
* Returns:
	* `SRCMSApp?`: An `SRCMSApp` object if the required keys are found in the JSON string, otherwise `null`.

#### fromJSON

`fun fromJSON(json: JSONObject): SRCMSApp?`

This method creates an `SRCMSApp` object from a JSON object.

* Parameters:
	* `json` (JSONObject): The JSON object representing the `SRCMSApp` object.
* Returns:
	* `SRCMSApp?`: An `SRCMSApp` object if the required keys are found in the JSON object, otherwise `null`.

## Constants

The companion object includes the following constants:

* `JSON_KEY_NAME` (String): Represents the key for the app name in the JSON object.
* `JSON_KEY_PACKAGE` (String): Represents the key for the package name in the JSON object.
* `JSON_KEY_REVISION` (String): Represents the key for the revision number in the JSON object.
* `JSON_KEY_VERSION` (String): Represents the key for the version name in the JSON object.
* `JSON_KEY_LAST_UPDATED` (String): Represents the key for the last updated date in the JSON object.
* `JSON_KEY_DESCRIPTION` (String): Represents the key for the description in the JSON object.

## Usage

```
import android.content.pm.PackageManager
import org.json.JSONObject
import java.util.*

// Create an instance of the SRCMSApp class
val appName = "MyApp"
val launchIntent: Intent? = // Define the launch intent
val icon: Drawable? = // Define the icon drawable
val srcmsApp = SRCMSApp(appName, launchIntent, icon)

// Set additional properties
srcmsApp.revision = 1L
srcmsApp.versionName = "1.0"
srcmsApp.lastUpdated = Date()
srcmsApp.description = "This is my app"
srcmsApp.packageString = "com.example.myapp"

// Retrieve the package name
val packageName = srcmsApp.getPackageName()

// Retrieve the launch intent
val packageManager: PackageManager = // Get the package manager
val launchIntent = srcmsApp.getLaunchIntent(packageManager)

// Convert the SRCMSApp object to JSON
val json: JSONObject = srcmsApp.toJSON()

// Create an SRCMSApp object from JSON
val jsonString: String = // Provide the JSON string
val fromJsonApp = SRCMSApp.fromJSON(jsonString)
```

Please note that some code sections are omitted and need to be replaced with actual implementation details