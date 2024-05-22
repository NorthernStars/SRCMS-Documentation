# SRCMS
The Android app in this Content Management System (CMS) for Social Robots consists of several main components involved in starting the app. The following section provides a detailed description of the app startup process, including the classes involved, their functions, and the specific lines of code.

## Main Classes

- **SocialRobotCMS:** The main class that manages the CMS startup process.
- **FragmentLoading:** This class manages the UI and performs the initialization, starting, and updating of the CMS.


## Startup-process of the App
The app's startup process is meticulously structured, encompassing several critical steps, each performing specific tasks to ensure the CMS is correctly initialized, started, and updated if necessary. The SocialRobotCMS class coordinates these processes, while the FragmentLoading class manages the user interface and interaction during these processes.

### 1. Initializing the CMS (`actionInit` Method)

The `actionInit` method of the `SocialRobotCMS` class is responsible for initializing the CMS. It consists of several key steps:

**Step 1: Notify Event Listeners**
- **Code:**
  ```kotlin
  srcmsCoreEventInitListeners.forEach { launchCoroutine({ it.onSRCMSInitStarting(srcms, config) }) }
  ```
- **Description:** All registered init listeners are notified that the initialization is starting. These listeners perform specific actions, such as displaying loading screens or logging the initialization status.

**Step 2: Load Configuration**
- **Code:**
  ```kotlin
  if (srcms.loadConfig(config)) {
      ...
  }
  ```
- **Description:** The `loadConfig` method is called to load the CMS configuration. If no configuration is provided, it attempts to load a saved default configuration.

**Step 3: Verify WiFi Connection**
- **Code:**
  ```kotlin
  if (srcms.verifyWifi("ROBUST", true)) {
      ...
  }
  ```
- **Description:** Checks if the device is connected to the "ROBUST" WiFi network. If not, it disables and re-enables WiFi to establish a connection.

**Step 4: Load User Database**
- **Code:**
  ```kotlin
  if (srcms.loadUserDB(srcms.config)) {
      ...
  }
  ```
- **Description:** Loads the user database based on the configuration. This is necessary to provide user information for the CMS.

**Step 5: Initialize Robot**
- **Code:**
  ```kotlin
  srcms.robot = SRCMSRobot()
  if (robotPreferences.isEmpty()) {
      ...
  } else {
      ...
  }
  ```
- **Description:** Initializes the robot functions with the provided preferences. If no preferences are provided, a default robot is initialized. Specific functions of the robot are configured here.

### 2. Starting the CMS (`actionStart` Method)

The `actionStart` method starts the CMS after successful initialization.

**Step 1: Notify Event Listeners**
- **Code:**
  ```kotlin
  srcmsCoreEventStartListeners.forEach { launchCoroutine({ it.onSRCMSStarting(srcms, config, user) }) }
  ```
- **Description:** Notifies all registered start listeners that the CMS start process has begun. These listeners can perform specific actions, such as displaying progress indicators or logging the start status.

**Step 2: Log in User**
- **Code:**
  ```kotlin
  // TODO: login user
  ```
- **Description:** This part is not yet implemented, but it is intended to log in the user to load personalized settings and data.

**Step 3: Check Local Apps**
- **Code:**
  ```kotlin
  if (updateInstalledApps()) {
      ...
  }
  ```
- **Description:** Updates the list of installed apps on the device. This method checks the installed applications and updates the CMS database accordingly.

### 3. Updating the CMS (`actionUpdate` Method)

The `actionUpdate` method updates the CMS by initiating the update process.

**Step 1: Start Update Process**
- **Code:**
  ```kotlin
  updateProcess = SRCMSUpdateProcess(...)
  updateProcess?.let { process -> 
      if (process.getStatus() == STATUS.IDLE) {
          return process.startProcess()
      }
  }
  ```
- **Description:** Initializes the update process if one does not already exist and starts it. The update process includes downloading and installing new versions of CMS apps and other relevant components.

### 4. Display and Progress Tracking (`FragmentLoading` Class)

The `FragmentLoading` class manages the user interface during the initialization, start, and update of the CMS.

**Step 1: onViewCreated**
- **Code:**
  ```kotlin
  override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
      super.onViewCreated(view, savedInstanceState)
      binding.pgbLoading.progress = 0
      binding.pgbLoading.max = 0
  }
  ```
- **Description:** Initializes the UI components, such as the progress bar, once the fragment is created.

**Step 2: onResume**
- **Code:**
  ```kotlin
  override fun onResume() {
      super.onResume()
      viewModel.getSRCMS()?.let { cms ->
          cms.addSRCMSCoreEventInitListener(this)
          cms.addSRCMSCoreEventStartListener(this)
          cms.addSRCMSCoreEventUpdateListener(this)

          when (arguments.action) {
              SRCMSAction.INIT -> viewModel.viewModelScope.launch(Dispatchers.Default) {
                  cms.actionInit(robotPreferences = (requireActivity() as MainActivity).getRobotPreferences())
              }
              SRCMSAction.START -> viewModel.viewModelScope.launch(Dispatchers.Default) {
                  cms.actionStart(config = cms.config)
              }
              SRCMSAction.UPDATE -> viewModel.viewModelScope.launch {
                  cms.actionUpdate()
              }
              ...
          }
      }
  }
  ```
- **Description:** This method is called when the fragment becomes visible. Depending on the passed arguments, a specific action (initialization, start, or update) is executed.

**Step 3: Update Progress Bar**
- **Code:**
  ```kotlin
  private fun updateProgress(action: SRCMSAction? = null) {
      viewModel.getSRCMS()?.let {
          activity?.runOnUiThread {
              binding.pgbLoading.max = SocialRobotCMS.actionMaximumSteps[action ?: arguments.action] ?: 0
              binding.pgbLoading.progress = SocialRobotCMS.actionActualSteps[arguments.action] ?: 0
              binding.pgbLoading.invalidate()
          }
      }
  }
  ```
- **Description:** Updates the progress bar based on the current progress of the ongoing action (initialization, start, or update).

**Step 4: Update UI with Information**
- **Code:**
  ```kotlin
  private fun infoText(text: String) {
      activity?.runOnUiThread {
          binding.txtLoadingInfo.text = text
          binding.txtLoadingInfo.invalidate()
      }
  }
  ```
- **Description:** Updates the UI component that displays the current status of the process. This can be an informative message or a status update.
