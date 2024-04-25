# SRCMSUser

The SRCMSUser class represents a user in the SocialRobotCMS system. Each user has a unique ID and can have a name, status, permissions, and a PIN. The class provides methods for converting user data to JSON format, loading user data from the filesystem, and generating IDs and PINs. It also includes enums for user permissions, user types, and user status.

## Constructors

The `SRCMSUser` class has a primary constructor with the following parameters:

* `id` (Long): The unique ID of the user. It has a default value of -1 if not provided.
* `name` (String): The name of the user. It has a default value of "user" if not provided.
* `status` (STATUS): The status of the user. It has a default value of `STATUS.INACTIVE` if not provided.
* `permissions` (Int): The permissions of the user. It has a default value of 0 if not provided.
* `pin` (Int?): The PIN of the user. It can be null if not provided

## Properties

The SRCMSUser class includes the following properties:

* `data` - `MutableMap<String, Any>`: A mutable map to store additional data associated with the user.


## Methods

The `SRCMSUser` class provides the following methods:

#### toJSON

`fun toJSON(): JSONObject`

This method converts the user data to a JSON object and returns it as a `JSONObject` instance.

#### loadUserData

`fun loadUserData(): Boolean`

This method loads the user data from the filesystem. It returns `true` if the data is loaded successfully, and `false` otherwise.

#### toString

`override fun toString(): String`

This method overrides the `toString()` function and returns a string representation of the user object. Itincludes the user data, PIN, and additional data (if available).


## Companion Object

The `SRCMSUser` class includes a companion object that provides static functions and constants:

#### fromJSON

`fun fromJSON(string: String): SRCMSUser?`

This function converts a JSON string to an `SRCMSUser` object. It takes a string parameter containing the JSON data and returns an `SRCMSUser` object if the required keys are found in the JSON.

#### fromJSON

`fun fromJSON(json: JSONObject): SRCMSUser?`

This function converts a `JSONObject` to an `SRCMSUser` object. It takes a `JSONObject` parameter containing the JSON data and returns an `SRCMSUser` object if the required keys are found in the JSON.

#### generatePin

`fun generatePin(userDatabase: MutableMap<Int, SRCMSUser>?): Int`

This function generates a unique PIN for a user. It takes a mutable map of `SRCMSUser` objects as a parameter to check for duplicate PINs. It returns a valid PIN that is not already set for any other user in the map.

#### isPinValid

`private fun isPinValid(pin: Int, db: MutableMap<Int,SRCMSUser>?): Boolean`

This function checks if a PIN is valid. It takes a PIN and a mutable map of `SRCMSUser` objects as parameters to check if the PIN is already set for any other user in the map. It returns `true` if the PIN is valid and not already set, and `false` otherwise.

#### generateID

`fun generateID(userdata: MutableMap<Int, SRCMSUser>?): Long`

This function generates a unique ID for a user. It takes a mutable map of `SRCMSUser` objects as a parameter to check for duplicate IDs. It returns a valid ID that is not already set for any other user in the map.

#### isIDValid

`private fun isIDValid(id: Long, db: MutableMap<Int, SRCMSUser>?): Boolean`

This function checks if an ID is valid. It takes an ID and a mutable map of `SRCMSUser` objects as parameters to check if the ID is already set for any other user in the map. It returns `true` if the ID is valid and not already set, and `false` otherwise.


## Enumerations

The `SRCMSUser` class includes the following enums:

### UserPermission

This enum represents user permissions and includes the following flags:

* `IS_ROOT`: Permission flag for root access.
* `CAN_LIST_USERS`: Permission flag for listing users.
* `CAN_EDIT_USERS`: Permission flag for editing users.
* `CAN_TRIGGER_APP_UPDATE`: Permission flag for triggering app updates.
* `CAN_EDIT_APP_UPDATE_REPOSITORIES`: Permission flag for editing app update repositories.
* `CAN_TRIGGER_CORE_UPDATE`: Permission flag for triggering core updates.
* `CAN_EDIT_CORE_UPDATE_REPOSITORY`: Permission flag for editing core update repositories.
* `CAN_LIST_APPS`: Permission flag for listing apps.
* `CAN_DELETE_APPS`: Permission flag for deleting apps.
* `CAN_ACCESS_SETTINGS`: Permission flag for accessing settings.
* `CAN_EDIT_ROBOT_SETTINGS`: Permission flag for editing robot settings.
* `CAN_EDIT_CMS_SETTINGS`: Permission flag for editing CMS settings.

### USERTYPE

This enum represents user types and includes the following values:

* `NORMAL`: Normal user type.
* `ADMIN`: Admin user type.

### STATUS

This enum represents user status and includes the following values:

* `LOGEDIN`: User is logged in.
* `ACTIVE`: User is active.
* `INACTIVE`: User is inactive

## Usage

```
import org.json.JSONObject

fun main() {
    // Creating a new SRCMSUser instance
	val user = SRCMSUser(name = "John Doe")
    
    // Converting user data to JSON
    val json = user.toJSON()
    println("User JSON: $json")
    
    // Creating a new SRCMSUser instance from JSON
    val jsonStr = 
    	"""{
            "id": 12345,
            "name": "Jane Smith",
            "status":"ACTIVE",
            "permissions":5
        }"""
        .trimIndent()
    
    val userFromJson = SRCMSUser.fromJSON(jsonStr)
    userFromJson?.let {
        println("User from JSON: $userFromJson")
    } ?: run {
    		println("Invalid JSON data")
    }
    
    // Generating a unique PIN
    val pin = SRCMSUser.generatePin(null)
    println("Generated PIN: $pin")
    
    // Generating a unique ID 
    val id = SRCMSUser.generateID(null)
    println("Generated ID: $id")
}
```

### Output

```
User JSON:
{
	"id":-1,"
	name":"John
	Doe","
	status":"
	INACTIVE","
	permissions":0
}

User from JSON: 
{
	"id":
	12345,"
	name":"Jane
	Smith","
	status":"
	ACTIVE","
	permissions": 5
} | pin = null

Generated PIN: 123456
Generated ID: 87654
```

> **_NOTE:_** In the example above, `SRCMSUser.generatePin()` and `SRCMSUser.generateID()` are called with `null` for the user database parameter, which means they are not checking for duplicate PINs or IDs. In a real scenario, you would pass a user database map to ensure uniqueness among existing users.