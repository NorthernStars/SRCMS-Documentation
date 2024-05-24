# Overview of `SRCMSCoreEvents` Class

The `SRCMSCoreEvents` class defines various listener interfaces to handle different events within the `SocialRobotCMS` application. These interfaces provide callback methods for different stages and actions related to the initialization, start, and update processes of the CMS.

## InitListener Interface

### Purpose
Handles events related to the initialization of the `SocialRobotCMS`.

### Methods
- **onSRCMSInitStarting(cms: SocialRobotCMS, config: SRCMSConfig?)**: Called when initialization starts.
- **onSRCMSInitFailed(cms: SocialRobotCMS, config: SRCMSConfig?)**: Called when initialization fails.
- **onSRCMSInitiated(cms: SocialRobotCMS, config: SRCMSConfig)**: Called when initialization is completed.
- **onSRCMSRobotInitStarting(cms: SocialRobotCMS)**: Called when robot initialization starts.
- **onSRCMSRobotInitFailed(cms: SocialRobotCMS)**: Called when robot initialization fails.
- **onSRCMSRobotInitiated(cms: SocialRobotCMS)**: Called when robot initialization is completed.
- **onSRCMSConfigReading(cms: SocialRobotCMS)**: Called when configuration reading starts.
- **onSRCMSConfigReadingFailed(cms: SocialRobotCMS)**: Called when configuration reading fails.
- **onSRCMSConfigRead(cms: SocialRobotCMS, config: SRCMSConfig)**: Called when configuration is read successfully.
- **onSRCMSUserDBLoading(cms: SocialRobotCMS, config: SRCMSConfig?)**: Called when the user database loading starts.
- **onSRCMSUserDBLoadingFailed(cms: SocialRobotCMS, config: SRCMSConfig?)**: Called when the user database loading fails.
- **onSRCMSUserDBLoaded(cms: SocialRobotCMS, config: SRCMSConfig)**: Called when the user database is loaded successfully.
- **onSRCMSWifiVerify(cms: SocialRobotCMS)**: Called when Wi-Fi verification starts.
- **onSRCMSWifiVerifyFailed(cms: SocialRobotCMS)**: Called when Wi-Fi verification fails.
- **onSRCMSWifiVerifySuccess(cms: SocialRobotCMS)**: Called when Wi-Fi verification succeeds.

## StartListener Interface

### Purpose
Handles events related to the starting process of the `SocialRobotCMS`.

### Methods
- **onSRCMSStarting(cms: SocialRobotCMS, config: SRCMSConfig?, user: SRCMSUser?)**: Called when the CMS starts.
- **onSRCMSStartingFailed(cms: SocialRobotCMS, config: SRCMSConfig?, user: SRCMSUser?)**: Called when starting the CMS fails.
- **onSRCMSStarted(cms: SocialRobotCMS, config: SRCMSConfig, user: SRCMSUser?)**: Called when the CMS is successfully started.
- **onSRCMSRemoteServiceStart(cms: SocialRobotCMS, config: SRCMSConfig?, user: SRCMSUser?)**: Called when the remote service starts.
- **onSRCMSUserLogin(cms: SocialRobotCMS)**: Called when a user login attempt occurs.
- **onSRCMSUserLoginFailed(cms: SocialRobotCMS, user: SRCMSUser?)**: Called when a user login attempt fails.
- **onSRCMSUserLoginSuccess(cms: SocialRobotCMS, user: SRCMSUser)**: Called when a user login attempt succeeds.
- **onSRCMSLocalAppsChecking(cms: SocialRobotCMS)**: Called when checking local apps starts.
- **onSRCMSLocalAppsCheckingFailed(cms: SocialRobotCMS)**: Called when checking local apps fails.
- **onSRCMSLocalAppsChecked(cms: SocialRobotCMS)**: Called when checking local apps is completed.

## UpdateListener Interface

### Purpose
Handles events related to the update process of the `SocialRobotCMS`.

### Methods
- **onSRCMSRepositoryUpdateProcessStart(cms: SocialRobotCMS)**: Called when the update process starts.
- **onSRCMSRepositoryUpdateProcessRepositoryCheck(cms: SocialRobotCMS, repository: SRCMSRepository)**: Called when checking a repository for updates starts.
- **onSRCMSRepositoryUpdateProcessRepositoriesCheckedUpdatesFound(cms: SocialRobotCMS, numOfApps: Int)**: Called when updates are found after checking all repositories.
- **onSRCMSRepositoryUpdateProcessRepositoriesCheckedNoUpdates(cms: SocialRobotCMS)**: Called when no updates are found after checking all repositories.
- **onSRCMSRepositoryUpdateProcessAppDownloadStart(cms: SocialRobotCMS, repository: SRCMSRepository, newApp: SRCMSAppInfo, oldApp: SRCMSApp? = null)**: Called when downloading an app starts.
- **onSRCMSRepositoryUpdateProcessAppDownloadFailed(cms: SocialRobotCMS, repository: SRCMSRepository, newApp: SRCMSAppInfo, oldApp: SRCMSApp? = null)**: Called when downloading an app fails.
- **onSRCMSRepositoryUpdateProcessAppDownloadSuccess(cms: SocialRobotCMS, repository: SRCMSRepository, newApp: SRCMSAppInfo, oldApp: SRCMSApp? = null)**: Called when downloading an app succeeds.
- **onSRCMSRepositoryUpdateProcessAppInstallLaunched(cms: SocialRobotCMS, repository: SRCMSRepository, newApp: SRCMSAppInfo, oldApp: SRCMSApp? = null)**: Called when installing an app starts.
- **onSRCMSRepositoryUpdateProcessInstallReturned(cms: SocialRobotCMS)**: Called when the installation process returns.
- **onSRCMSRepositoryUpdateProcessAppUpdateNext(cms: SocialRobotCMS)**: Called when the next app update can proceed.
- **onSRCMSRepositoryUpdateProcessDone(cms: SocialRobotCMS)**: Called when all apps from all repositories are updated.
- **onSRCMSRepositoryUpdateProcessFailed(cms: SocialRobotCMS)**: Called when the update process fails.

## Conclusion

The `SRCMSCoreEvents` class provides a structured way to handle various events in the `SocialRobotCMS` application by defining listener interfaces. These interfaces ensure that different stages and actions in the initialization, start, and update processes are appropriately handled and logged, enhancing the maintainability and robustness of the application.
