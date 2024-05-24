The `SRCMSUpdateHandlerListener` interface is designed to listen to events related to the update handling process within the `SocialRobotCMS` system. It contains methods that are called when certain update-related events occur, such as when there are no updates available or when the update process results are available.

Here is an overview of the `SRCMSUpdateHandlerListener` interface and its components:

## SRCMSUpdateHandlerListener Interface

### Purpose
To provide a mechanism for listening to events related to the update handling process in the `SocialRobotCMS` system.

### Methods
- **onSRCMSAppUpdateHandlerNoUpdate(repo: SRCMSRepository?)**: Called when there are no updates available for a given repository.
- **onSRCMSUpdateHandlerUpdateResult(repo: SRCMSRepository?, appInfo: MutableMap<SRCMSAppInfo, SRCMSApp?>?)**: Called when the update process results are available. This provides the repository and a map containing the update information for each app.

### Code Implementation

```kotlin
package de.fhkiel.srcms.core.listener

import de.fhkiel.srcms.core.repository.SRCMSRepository
import de.fhkiel.srcms.lib.data.SRCMSApp
import de.fhkiel.srcms.lib.data.SRCMSAppInfo

/**
 * Listener interface to listen to [SRCMSUpdateHandlerListener] events.
 */
interface SRCMSUpdateHandlerListener {
    /**
     * Called when there are no updates available for a given repository.
     *
     * @param repo The repository for which there are no updates, or null.
     */
    fun onSRCMSAppUpdateHandlerNoUpdate(repo: SRCMSRepository?)

    /**
     * Called when the update process results are available.
     *
     * @param repo The repository for which the update results are available, or null.
     * @param appInfo A map containing the update information for each app, or null.
     */
    fun onSRCMSUpdateHandlerUpdateResult(repo: SRCMSRepository?, appInfo: MutableMap<SRCMSAppInfo, SRCMSApp?>?)
}
```

## Usage Example

To use the `SRCMSUpdateHandlerListener`, you would need to implement this interface in a class that should handle the update events. Here is an example of how you might implement and use this interface:

```kotlin
class MyUpdateHandlerListener : SRCMSUpdateHandlerListener {
    override fun onSRCMSAppUpdateHandlerNoUpdate(repo: SRCMSRepository?) {
        // Handle the event when there are no updates
        if (repo != null) {
            println("No updates available for repository: ${repo.name}")
        } else {
            println("No updates available.")
        }
    }

    override fun onSRCMSUpdateHandlerUpdateResult(repo: SRCMSRepository?, appInfo: MutableMap<SRCMSAppInfo, SRCMSApp?>?) {
        // Handle the update results
        if (repo != null && appInfo != null) {
            println("Update results for repository: ${repo.name}")
            appInfo.forEach { (appInfo, app) ->
                println("App: ${appInfo.name}, Current Version: ${app?.version ?: "None"}, New Version: ${appInfo.version}")
            }
        } else {
            println("Update results are not available.")
        }
    }
}

// Usage
fun main() {
    val listener = MyUpdateHandlerListener()

    // Simulate no updates available
    listener.onSRCMSAppUpdateHandlerNoUpdate(null)

    // Simulate update results
    val repo = SRCMSRepository("ExampleRepo")
    val appInfo = mutableMapOf<SRCMSAppInfo, SRCMSApp?>(
        SRCMSAppInfo("App1", "1.1") to SRCMSApp("App1", "1.0")
    )
    listener.onSRCMSUpdateHandlerUpdateResult(repo, appInfo)
}
```

In this example, `MyUpdateHandlerListener` implements the `SRCMSUpdateHandlerListener` interface. The `onSRCMSAppUpdateHandlerNoUpdate` method is implemented to handle the event when there are no updates available, and the `onSRCMSUpdateHandlerUpdateResult` method is implemented to handle the update results. The main function simulates both events to demonstrate how the listener might be used in practice.
