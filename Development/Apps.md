# Apps

## Overview


| App/Module   |      Description      |  Using Module |
|----------|---------------| -------------|
| ABC App | At the touch of a button, the application generates a random letter and reads it out loud, either with or without a spelling board. A new letter can then be drawn or the current letter can be read out again. | / |
| Audio Quiz | The robot plays a sound, then the participants have to guess what the sound was. The sounds are divided into categories (e.g. animal sounds) | Content Player Quiz|
| Character Quiz | The robot gradually gives a clue (at the touch of a button) that points to an object, an event, etc. beginning with a certain letter (selected prior). If the participants think they know the solution they are looking for, the puzzle can be solved at the touch of a button. | Content Player Quiz |
| Chess Game | Chess can be played against the robot on the tablet according to official rules. The pieces are moved by tapping them and the robot motivates the user in between. | / |
| Communication App | The operator can enter a text, which the robot then speaks at the touch of a button. | / |
| Content Player [Module] | The robot displays a selection of audio content sorted by category on the tablet. By tapping the corresponding button, the content is played and the robot makes supporting movements. | / |
| Content Player Quiz [Module] | The robot reads out a question, which is displayed. The answer to the question can be revealed if required and the next question is asked. | / |
| Happy Birthday | The robot says a birthday greeting to a person whose name was previously entered. A birthday song is then played, which the user must first select from two songs. Meanwhile, one or more previously selected images are displayed on the tablet. | / |
| Hint Quiz | The robot gradually gives a clue (at the touch of a button) that points to an object, an event, etc. If the participants think they know the term they are looking for, the puzzle can be solved at the touch of a button. | Content Player Quiz |
| Jukebox | The application contains various songs, organized in categories, to play and sing along to. The robot can make dance movements and rotate. | Content Player |
| Keyword Quiz | The robot gradually gives a clue (at the touch of a button) that points to an object, an event, etc. of a certain topic (selected prior). If the participants think they know the solution they are looking for, the puzzle can be solved at the touch of a button. | Content Player Quiz |
| Macarena Dance | The robot plays the song "Macarena" and makes the movements of the corresponding dance. | / |
| Meditation | In the app, you can choose between meditations and dream journeys. Content that can be played can be found under the respective category. | Content Player |
| Poems | The application can play audio files with poems. Optionally with or without gestures. | Content Player | 
| Proverb | The robot says the first part of a proverb and the participants then have to complete the proverb. At the touch of a button, the robot reads out the solution. The quiz is divided into different categories of proverbs. | Content Player Quiz |
| Quiz | The robot asks and shows a riddle question. The solution is displayed at the touch of a button. | Content Player Quiz |
| Rabbit Game | The user must "catch" rabbits that appear on the screen. Tapping on the rabbits makes them disappear, but they gradually appear faster and faster. If too many rabbits have not been tapped, the game ends. | / |
| Remember Quiz | The robot reads out a story that the participants should listen to carefully. The robot then asks questions about the content of the story, which the participants have to answer from memory. At the touch of a button, the robot gives the correct answer. | Content Player Quiz |
| Storytelling | The application can play audio files with stories. Optionally with or without gestures. | Content Player |
| Workout App | The robot demonstrates various movement exercises for the upper body (including arms and hands), which the user is asked to imitate. There are both individual exercises and ready-made workouts with different levels of difficulty. | / |





## Creating a new App

### Simple App

#### Get started
1. Create a new project: <br> `File` &rarr; `New` &rarr; `New Project...` &rarr; `Phone & Tablet` &rarr; `Empty Activity`
2. Click `Next` to name your application and set the package name according to the correct app category: <br> `de.fhkiel.srcms.apps.[category].p.APPNAME`

> **_NOTE:_**  If programming for Pepper: Select minimum SDK &rarr; `API 23: Android 6.0 (Marshmallow)`.

3. Click `Finish`.

> **_NOTE:_**  Make sure to extend your MainActivity from `SRCMSActivity()`


#### Dependencies & Plugins
Add following dependencies to your project's `build.gradle`:
```
dependencies {
    classpath "androidx.navigation:navigation-safe-args-gradle-plugin:2.7.7"
    classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:1.8.10"
}
```

Add following dependencies and plugins to your application's `build.gradle`:
```
dependencies {
    implementation 'de.fhkiel.srcms.lib:srcmslib:0.1.8'
    
    implementation 'com.aldebaran:qisdk:1.7.5'
    implementation 'com.aldebaran:qisdk-design:1.7.5'
    coreLibraryDesugaring 'com.android.tools:desugar_jdk_libs:2.0.4'
    ...
}
```

```

plugins {
    id 'androidx.navigation.safeargs.kotlin'
    ...
}

```

> **_NOTE:_**  Make sure to use Android Gradle Plugin Version `8.0.2` or higher, and Gradle Version `8.1` or higher


### Using Content Player Module

The new application provides the content player module with the necessary information to function as a media player. All functionalities are within the content player module.

#### Get started
1. Create a new module within the `Content Player` project: <br> `File` &rarr; `New` &rarr; `New Module...` &rarr; `Phone & Tablet` 
2. Name your application and set the package name according to the correct app category: <br> `de.fhkiel.srcms.apps.[category].p.APPNAME`

> **_NOTE:_**  If programming for Pepper: Select minimum SDK &rarr; `API 23: Android 6.0 (Marshmallow)`.

3. Click `Next`, select `Empty Activity` and `Finish`.

#### Dependencies & Plugins
Add following dependencies and plugins to your application's `build.gradle`:
```
dependencies {
    implementation 'de.fhkiel.srcms.lib:srcmslib:0.1.8'
    implementation project(path: ':contentplayer')
    implementation project(path: ':assets')

    implementation 'com.aldebaran:qisdk:1.7.5'
    implementation 'com.aldebaran:qisdk-design:1.7.5'
    coreLibraryDesugaring 'com.android.tools:desugar_jdk_libs:2.0.4'
    ...
}
```

```

plugins {
    id 'androidx.navigation.safeargs.kotlin'
    ...
}

```

> **_NOTE:_**  Make sure to use Android Gradle Plugin Version `8.0.2` or higher, and Gradle Version `8.1` or higher

#### Setting up MainActivity layout and programming file

1. In your MainActivity layout file, add the Navigation Component `FragmentContainerView`: <br> 
```
    <androidx.fragment.app.FragmentContainerView
        android:id="@+id/nav_host_fragment"
        android:name="androidx.navigation.fragment.NavHostFragment"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:defaultNavHost="true"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:navGraph="@navigation/nav_graph_content_player" />
```

2. In your MainActivity programming file, extend from `SRCMSActivity()` and implement the necessary member functions.
3. Declare and define following variables for the navigation components and information transfer:
```
private lateinit var navController: NavController
private lateinit var navHostFragment: NavHostFragment
private val viewModel : ContentPlayerViewModel by viewModels()
```
The `viewModel` can be used to set information for the content player. Following data can be set:
```
defaultLink: String 			// Link to download content
contentPath: String 			// Path to where content is stored
drawableResourceAlbum: Int? 	// Resource id from album image
drawableResourceMedia: Int? 	// Resource id from media image
listAnimationIds: List<Int>?	// List of resource ids for the robot animations
resourceIdRotation: Int?		// Resource id from robot rotation
automaticModeEnabled: Boolean 	// Flag whether to use automatic mode or not
```
> **_NOTE:_**  Data should be set in the `onResume()`.

4. Add following code to those member functions:
```
// setting theme
override fun getTheme(): Resources.Theme {
    val theme = super.getTheme()
    theme.applyStyle(applicationInfo.theme, true)

    return theme
}

// setting version name
override fun getVersionName(): String {
    return BuildConfig.VERSION_NAME
}

// launches content player
override fun launchApp() {
    navController.navigate(FragmentContentPlayer.launchContentPlayer())
}

```
5. Run your application.


### Using Content Player Quiz Module 
The new application provides the content player module quiz with the necessary information to function as a quiz app.

#### Get started
1. Create a new module within the `Quizzes` project: <br> `File` &rarr; `New` &rarr; `New Module...` &rarr; `Phone & Tablet` 
2. Name your application and set the package name according to the correct app category: <br> `de.fhkiel.srcms.apps.[category].p.APPNAME`

> **_NOTE:_**  If programming for Pepper: Select minimum SDK &rarr; `API 23: Android 6.0 (Marshmallow)`.

3. Click `Next`, select `Empty Activity` and `Finish`.

#### Dependencies & Plugins
Add following dependencies and plugins to your application's `build.gradle`:
```
dependencies {
    implementation 'de.fhkiel.srcms.lib:srcmslib:0.1.8'
    implementation project(path: ':contentplayerquiz')
    implementation files('libs/srcms-quiz-lib-6.jar')

    implementation 'com.aldebaran:qisdk:1.7.5'
    implementation 'com.aldebaran:qisdk-design:1.7.5'
    coreLibraryDesugaring 'com.android.tools:desugar_jdk_libs:2.0.4'
    ...
}
```

```

plugins {
    id 'androidx.navigation.safeargs.kotlin'
    ...
}

```

> **_NOTE:_**  Make sure to use Android Gradle Plugin Version `8.0.2` or higher, and Gradle Version `8.1` or higher

#### Setting up MainActivity layout and programming file

1. In your MainActivity layout file, add the Navigation Component `FragmentContainerView`: <br> 
```
   <androidx.fragment.app.FragmentContainerView
        android:id="@+id/nav_host_fragment_container"
        android:name="androidx.navigation.fragment.NavHostFragment"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:defaultNavHost="true"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:navGraph="@navigation/nav_graph_content_player_quiz" />
```

2. In your MainActivity programming file, extend from `SRCMSActivity()` and implement the necessary member functions.
3. Declare and define following variables for the navigation components and information transfer:
```
private lateinit var navController: NavController
private lateinit var navHostFragment: NavHostFragment
private val viewModel : ContentPlayerViewModel by viewModels()
```
The `viewModel` can be used to set information for the content player quiz. Following data can be set:
```
contentControllerQuestion : ContentController // Control for questions
contentControllerAnswer : ContentController   // Control for answers

defaultLink: String 			// Link to download content
contentPath: String 			// Path to where content is stored
drawableAlbum: Drawable 		// Drawable resource for album image
drawableSolveButton: Drawable 	// Drawable resource for image on solve button
stringAppNameId: String 		// App name
var autoplay = functionalities	// Flag whether to use automatic mode or not
```
> **_NOTE:_**  Data should be set in the `onResume()`.

4. Add following code to those member functions:
```
// setting theme
override fun getTheme(): Resources.Theme {
    val theme = super.getTheme()
    theme.applyStyle(applicationInfo.theme, true)

    return theme
}

// setting version name
override fun getVersionName(): String {
    return BuildConfig.VERSION_NAME
}

// launches content player quiz
override fun launchApp() {
    navController.navigate(FragmentContentPlayer.launchContentPlayer())
}
```
#### Content Controller Files
The content controller files take care about loading and playing questions and answers.

1. Create two content controller files: <br> `ContentControllerQuestion(context: Context, srcmsRobot: SRCMSRobot?)` <br> `ContentControllerAnswer(context: Context, srcmsRobot: SRCMSRobot?)`
2. Both have to inherit from `ContentController()`.
3. Implement members and set up desired behavior.
> **_NOTE:_**  Both content controller files need a corresponding layout file that will be displayed within the content player quiz module. Set the layout view inside the `loadContent()` function.


4. Add both to the view model in `MainActivity` class, like:
```
viewModel.contentControllerQuestion = ContentControllerQuestion(this, getRobot())
viewModel.contentControllerAnswer = ContentControllerAnswer(this, getRobot())
```
5. Run your application.


## VCS
### Add Git version control

Now you project is ready for setting up Git and the first initial commit.

1. In Android Studio enable version control integration:
 `VCS` &rarr; `Enable Version Control Integration` &rarr; Select `Git`
2. Do your initial commit. You have three option to to it:<br>
    2.1. via menu: **Git > Commit** <br>
    2.2. via toolbar-icon: **Green Check Icon (Commit)** <br>
    2.3. via left sidebar: **Commit**

3. Check all unversioned files and add **Initial Commit** as commit message.
4. Commit the changes.
_If there are open ToDos, ignore them and **Commit Anyway**_

### Setup online repository

It is time to bring your project online and setup your Git repository.

1. Goto your projects Bitbucket repository and copy the clone URL.
2. In Android Studio, add it as remote URL for your project:
 `Git` &rarr; `Manage Remotes` &rarr; `Add`
3. Push you project changes. You have two options: <br>
    3.1. via menu: **Git > Push** <br>
    3.2. via toolbar-icon: **Green Arrow (Push)**

### Creating a development branch
Now we continue with repository setup and the dev branch:

1. In Android Studio open the branches view. You have two options: <br>
    1.1. via menu: **Git > Branches** <br>
    1.2. via bottom toolbar: click on **master** branch on very right of bottom toolbar of the window
2. Select `+ New Branch`
3. Enter new branch name **dev**
4. Make sure `Checkout branch` option is checked

You should be on the dev branch now (see branch name on very right bottom toolbar of the window).

Push the changes again to online repository (see above) and you are done with setting up your project and repository.

## Additional Information

### Packaging

The srcms lists the available apps using their package names.
Their package name must be one of the base package names, followed by a hierachy of categories and the apps private packages.

Package names are case insensitive.

They are explained in the following:

#### Base-Packages

Base packages are to build apps of different institutions or companies. The are the first packages any app, that should be shown in scrms, must use
as its own package name.

There can be multiple base package names allowed in an instance of the srcms. For the FH Kiel the default base package is:
`de.fhkiel.srcms.apps`

#### Apps category hierachy

The hierachy, the apps are displayed in, is build using their packages. Therefor each package, following the base package (see above), is a category
displayed in the srcms.
The categories are divided, like the packages, by a dot.

The name of a category defined by a package, can be translated by the srcms into any other human-radable name. Therefore the package names are
only for internal structual hierachy.

**Example**

An app with the the category hierachy

_Therapy Physical Dance_

must be using the following package (with default base package of FH Kiel):
`de.fhkiel.srcms.apps.therapy.physical.dance`

Attention: This must still be followed by a private package. See next section

#### Private packages

Each Android application must implement a custom package. So each app, besides the base package and the category hioerachy (see above), must
use a custom package. This custom (privat) package and all packages beklow, should not be displayd as category inside the srcms.

Therefore the privat package must be inside a package called _p_.

Everything inside this package is private and not visible to the user.

**Example**

Using the example above, extended by a private package for this particular app, it can look like this:
`de.fhkiel.srcms.apps.therapy.physical.p.workout`

### FH Kiel Catgories
The FH Kiel uses by default the following category hierachy:


| Name   |      Package name      | Description | Color Scheme |
|-----------|---------------| --------------- | -------------|
| Demo | de.fhkiel.srcms.apps.fun.p.APPNAME| Demonstration apps, for development only. | Default (Blue) |
| Therapy (Category) | de.fhkiel.srcms.apps.therapy.*| For different kind of therapy applications | Triadic Colors |
| Therapy Physical | de.fhkiel.srcms.apps.therapy.physical.p.APPNAME| For physical applications | Triadic Colors |
| Therapy Cognitive | de.fhkiel.srcms.apps.therapy.cognitive.p.APPNAME| For quizzes and cognative applications | Triadic Colors |
| Therapy Psyc | de.fhkiel.srcms.apps.therapy.psyc.p.APPNAME| Mindfullness apps | Triadic Colors |
| Sozio | de.fhkiel.srcms.apps.sozio.p.APPNAME| Sozio interaction, Infotainment apps | Analogous Blue |
| Fun | de.fhkiel.srcms.apps.fun.p.APPNAME| For fun applications | Analogous Green |
| Communication | de.fhkiel.srcms.apps.communication.p.APPNAME| Communication / Tele-presence / video call apps | Analogous Blue |


### Creating a Revision Task
To create a release, open Jira and open the Kanban board, that belongs to your project.
Follow these steps to create a release for your project.

1. Use the **Create** button (on Jira top navigation bar) to create a new task
2. Select: <br>
    **Issue Type**: Task <br>
    **Summary**: Your apps name and the revision number (e.g.: _Test App rev. 1_)<br>
    **Component**: Select your apps component (e.g.: _Test App_)<br>
    **Description**: If needed add one<br>
    **Fix Version/s**: Select a version where you want to publish your task / revision. It maybe is not specifiednow, so leave it blank.<br>
    **Priority**: Set an appropiate priority for the desire task<br>
    **Assignee**: Select the one, that should work on this task<br>

#### Schedule Task in Backlog

Now your task is in the board Backlog. We need to schedule it to be visible on the board and put it into development.

1. Goto the boards **Backlog** (on left toolbar)
2. **Drag** the revision task to **Scheduled** to plan it for development.
3. Go back to **Kanban board** (on left toolbar)

#### Start developing
In Kanban board, the task for revision one of yur app should now be visible in **Scheduled** column.
Now we put it into development and create a revision branch for further work.

1. **Drag** the revision task to column **In Development (Develop)**
2. **Click** on the revision task to open the task details view on the right side.
3. **Scroll down** to **Development** and click on **Create new branch**.<br>
Open it in a new tab, while it will open _Bitbucket_.
4. As **Repsitory** select your apps repository <br>
As **Branchtype** select Release <br>
As **Origin** select **dev**<br>
and create new branch.

You are done now and created your first revision task.
You can continue with working on features of your projects first revision.

### Working on features
Now you can start working on features of an revision.
To develop features, a revision has to be in development and a revision branch has to be created, before you can start with working on features.
Here are some smple rules to follow during working on a task. Here are only the basics explained.

1. For a new feature, **Create** a new **Task** in **Jira**
2. Set the task as **child of revision task**
3. Drag the task from **Backlog** to **Scheduled**, to start working on it
4. Create **new Branch** from **revision branch** for every task.<br>
If you **start working** on a task, always **merge** the **revision branch** into the **task branch** to sync to your latest revision work.
5. If you think you are done, do a Technical Test<br>
    5.1. **Drag** the feature task to the **Technical Test** column<br>
      *  5.1.1. If if succeeds: **drag** it to the **Done** column <br>
      *  5.1.2. If it fails: **drag** to back to **In Development (Fix)**
6. If a task is **complete** (column Done), **merge** the **task branch** into the **revision branch**