# SocialRobotCMS

The `SocialRobotCMS` class is the main class of the Social Robot Content Management System (CMS). It stores all configurations and handles all actions related to the CMS. This class enables interaction and control of a social robot system through various events and processes.

## Packages and Imports

The class imports a variety of Android and Java libraries as well as custom classes and interfaces necessary for the functionality of the CMS. Here are some of the key imports:

- `android.content.*`: Management of Android components and services
- `android.net.*`: Network connection management
- `android.os.*`: Operating system functions management
- `android.util.*`: Logging and debugging
- `androidx.activity.result.*`: Handling activity results
- `androidx.lifecycle.*`: Lifecycle management
- `androidx.preference.*`: Management of app preferences
- `kotlinx.coroutines.*`: Support for concurrent programming
- `org.json.*`: JSON processing

## Class Structure

### Properties

The `SocialRobotCMS` class contains several properties, including configuration objects, status variables, listener lists, and objects for managing the robot:

- `config`: The configuration object of the CMS.
- `status`: The current status of the CMS.
- `showAppsCategory`: The current app category.
- `activeUser`: The currently logged-in user.
- `robot`: The robot object.
- `updateProcess`: The update process.
- `srcmsCoreEventInitListeners`, `srcmsCoreEventStartListeners`, `srcmsCoreEventUpdateListeners`: Lists of event listeners.

### Methods

#### Initialization and Start

- `actionInit(config: SRCMSConfig? = null, robotPreferences: Map<RobotFunctionInterface.FUNCTIONS, Map<String, Any>>): Boolean`: This method initializes the CMS with the given configuration and robot preferences. It informs the listeners and verifies the Wi-Fi connection as well as the user database.
  
- `actionStart(config: SRCMSConfig? = null, user: SRCMSUser? = null): Boolean`: This method starts the CMS with the given configuration and logs in a user. It checks the installed apps and informs the listeners about the start process.

#### Update

- `actionUpdate(): Boolean`: Starts the update process of the CMS if it is not already running or completed.

#### Configuration and Data Management

- `loadConfig(config: SRCMSConfig?): Boolean`: Loads the configuration and creates repositories.
- `saveRemoteRepositories(repositories: MutableList<SRCMSRepository>)`: Saves a list of remote repositories.
- `loadUserDB(config: SRCMSConfig?): Boolean`: Loads the user database from the system.
- `loginUser(user: SRCMSUser): Boolean`: Logs in a user.
- `logoutUser(user: SRCMSUser?): Boolean`: Logs out a user.

#### App Management

- `updateInstalledApps(): Boolean`: Updates the list of installed apps.
- `getAppIntent(app: SRCMSApp, context: Context?): SRCMSAppIntent`: Generates an intent for a given app.

#### Network and Service Management

- `startRemoteService()`: Starts and binds the remote service.
- `stopRemoteService()`: Stops the remote service.
- `verifyWifi(wifiSsid: String, enableTimeout: Boolean = false): Boolean`: Verifies the Wi-Fi connection and ensures that the device is connected to the specified SSID.

### Helper Methods

- `toJSON(sharedPreferences: SharedPreferences?): JSONObject`: Generates a JSON object from shared preferences.
- `launchCoroutine(callable: suspend () -> Unit, dispatcher: CoroutineDispatcher = Dispatchers.Default)`: Launches a coroutine.
- `resetAction(action: SRCMSAction, maximumSteps: Int): SRCMSAction`: Resets the action steps.
- `incAction(action: SRCMSAction)`: Increments the action step.
- `getInstalledApps(packageManager: PackageManager, apps: List<ApplicationInfo>, allowedPackages: List<String>): MutableList<SRCMSApp>`: Returns a list of all installed CMS apps.

## Status Enums

The class defines various status values for the CMS system:

- `NONE`, `IDLE`
- `INIT_STARTED`, `INIT_DONE`, `INIT_FAILED`
- `STARTING`, `STARTED`, `START_FAILED`
- `UPDATE_STARTED`, `UPDATE_CHECK_REPOSITORIES`, `UPDATE_REPOSITORIES_CHECKED`, `UPDATE_APP_DOWNLOAD_NEXT`, `UPDATE_APP_DOWNLOAD_START`, `UPDATE_APP_DOWNLOAD_SUCCESS`, `UPDATE_APP_DOWNLOAD_FAILED`, `UPDATE_APP_INSTALL_LAUNCH`, `UPDATE_APP_INSTALL_RETURNED`, `UPDATE_DONE`, `UPDATE_FAILED`

## Conclusion

The `SocialRobotCMS` class provides a comprehensive implementation of a CMS for social robots, covering various aspects such as initialization, start, update, app management, and network management. The use of Kotlin coroutines enables efficient and responsive handling of concurrent tasks.