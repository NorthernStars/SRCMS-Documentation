The `SRCMSStatusChangeListener` interface is designed to listen for status changes in the `SocialRobotCMS` system. This interface contains a single method `onStatusChanged` that will be called whenever the status of the `SocialRobotCMS` changes. The `SRCMSStatusChangeEmitter` is a nested open class, which can be extended to provide additional functionality or context related to the status change events.

Here is an overview of the `SRCMSStatusChangeListener` interface and its components:

## SRCMSStatusChangeListener Interface

### Purpose
To provide a mechanism for listening to changes in the status of the `SocialRobotCMS`.

### Methods
- **onStatusChanged(emitter: SRCMSStatusChangeEmitter, status: SocialRobotCMS.STATUS)**: This method is called whenever the status of the `SocialRobotCMS` changes. It provides the new status and an emitter which can be used to provide additional context about the status change.

### Nested Classes
- **SRCMSStatusChangeEmitter**: An open class that can be extended to provide additional functionality or context related to the status change events.

### Code Implementation

```kotlin
package de.fhkiel.srcms.core.listener

import de.fhkiel.srcms.core.SocialRobotCMS

/**
 * Listener interface to listen to [SocialRobotCMS.STATUS] changes.
 */
interface SRCMSStatusChangeListener {
    /**
     * Called when the status of [SocialRobotCMS] changes.
     *
     * @param emitter The source of the status change.
     * @param status The new status of the SocialRobotCMS.
     */
    fun onStatusChanged(emitter: SRCMSStatusChangeEmitter, status: SocialRobotCMS.STATUS)

    /**
     * Open class that can be extended to provide additional functionality or context
     * related to the status change events.
     */
    open class SRCMSStatusChangeEmitter
}
```

## Usage Example

To use the `SRCMSStatusChangeListener`, you would need to implement this interface in a class that should handle status change events. Here is an example of how you might implement and use this interface:

```kotlin
class MyStatusChangeListener : SRCMSStatusChangeListener {
    override fun onStatusChanged(emitter: SRCMSStatusChangeEmitter, status: SocialRobotCMS.STATUS) {
        // Handle the status change here
        println("Status changed to: $status")
    }
}

class MyStatusChangeEmitter : SRCMSStatusChangeListener.SRCMSStatusChangeEmitter() {
    // Additional functionality for the emitter can be added here
}

// Usage
fun main() {
    val listener = MyStatusChangeListener()
    val emitter = MyStatusChangeEmitter()
    
    // Simulate a status change
    listener.onStatusChanged(emitter, SocialRobotCMS.STATUS.INITIALIZING)
}
```

In this example, `MyStatusChangeListener` implements the `SRCMSStatusChangeListener` interface, and `MyStatusChangeEmitter` extends the `SRCMSStatusChangeEmitter` class to provide additional functionality if needed. The `onStatusChanged` method is implemented to handle the status changes accordingly.
