The `SRCMSBaseProcess` class is a base class designed to manage the status of a process within the `SocialRobotCMS` system. It utilizes Kotlin coroutines to handle asynchronous operations and dispatch status changes to registered listeners.

Here's an overview of the `SRCMSBaseProcess` class and its components:

## SRCMSBaseProcess Class

### Purpose
To provide a base class for processes within the `SocialRobotCMS` system, managing status changes and notifying listeners.

### Components

1. **Properties**
    - `cms`: The `SocialRobotCMS` instance that this process is associated with.
    - `statusChangeListener`: A mutable list of listeners that will be notified when the status changes.
    - `status`: The current status of the process, initially set to `SocialRobotCMS.STATUS.IDLE`.

2. **Functions**
    - `getStatus()`: Returns the current status of the process.
    - `changeStatus(status: SocialRobotCMS.STATUS)`: Changes the status of the process and notifies all registered listeners using coroutines.
    - `launchCoroutine(callable: suspend () -> Unit, dispatcher: CoroutineDispatcher)`: Launches a coroutine for asynchronous operations, with a default dispatcher of `Dispatchers.Default`.

### Code Implementation

```kotlin
package de.fhkiel.srcms.core.process

import de.fhkiel.srcms.core.SocialRobotCMS
import de.fhkiel.srcms.core.listener.SRCMSStatusChangeListener
import kotlinx.coroutines.CoroutineDispatcher
import kotlinx.coroutines.Dispatchers

@Suppress("unused")
open class SRCMSBaseProcess(
    private val cms: SocialRobotCMS,
    private val statusChangeListener: MutableList<SRCMSStatusChangeListener> = mutableListOf()
) : SRCMSStatusChangeListener.SRCMSStatusChangeEmitter() {
    private var status: SocialRobotCMS.STATUS = SocialRobotCMS.STATUS.IDLE

    fun getStatus(): SocialRobotCMS.STATUS {
        return this.status
    }

    protected fun changeStatus(status: SocialRobotCMS.STATUS) {
        this.status = status
        statusChangeListener.forEach {
            SocialRobotCMS.launchCoroutine({
                it.onStatusChanged(
                    this,
                    this.status
                )
            }, Dispatchers.Default)
        }
    }

    protected fun launchCoroutine(callable: suspend () -> Unit, dispatcher: CoroutineDispatcher = Dispatchers.Default) {
        SocialRobotCMS.launchCoroutine(callable, dispatcher)
    }
}
```

## Explanation

- **Status Management**: The `status` property holds the current status of the process, and the `getStatus()` function allows retrieving this status.
- **Status Change Notification**: The `changeStatus()` function updates the `status` property and notifies all registered listeners by launching a coroutine for each listener. This ensures that the notification process is handled asynchronously.
- **Coroutine Launching**: The `launchCoroutine()` function is a helper function that delegates the coroutine launching to the `SocialRobotCMS` class, allowing for easy execution of asynchronous tasks.

## Usage Example

Here's an example of how you might extend the `SRCMSBaseProcess` class to create a specific process that changes its status:

```kotlin
class MyProcess(cms: SocialRobotCMS) : SRCMSBaseProcess(cms) {
    fun startProcess() {
        changeStatus(SocialRobotCMS.STATUS.STARTING)
        launchCoroutine({
            // Simulate some work
            delay(1000)
            changeStatus(SocialRobotCMS.STATUS.RUNNING)
        })
    }
}

// Usage
fun main() {
    val cms = SocialRobotCMS()
    val process = MyProcess(cms)

    // Add a status change listener
    process.statusChangeListener.add(object : SRCMSStatusChangeListener {
        override fun onStatusChanged(emitter: SRCMSStatusChangeEmitter, status: SocialRobotCMS.STATUS) {
            println("Status changed to: $status")
        }
    })

    // Start the process
    process.startProcess()
}
```

In this example, `MyProcess` extends `SRCMSBaseProcess` and provides a `startProcess()` method that changes the status to `STARTING`, performs some work asynchronously, and then changes the status to `RUNNING`. The main function creates an instance of `MyProcess`, adds a status change listener, and starts the process, demonstrating how the status changes are handled and notified.
