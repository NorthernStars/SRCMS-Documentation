# Development
You want to develop an Android application for the Social Robot CMS (SRCMS)?

Follow the guidelines on this page, as well as on the subpages, to learn how to develop this kind of
application.

## Getting started
1. Download The srcms-lib regarding its installation guide: SRCMS-Library
2. Download the demo projects for Kotlin or Java, regarding you favorite programming language: Demo-Apps
3. If not already available, create a new virtual device of the robots tablet for testing: Apps
4. Open one of the demo apps and launch them.

## Development
To develop apps for the Social Robot CMS, use the following workflow.

### Tools
For developing we use Bitbucket (GIT) as software repository to store the code changes (see https://confluence.iue.fh-kiel.de/display/IuERL
/Git+Software+Repository),
Jira for managing the project development lifecycle using a KanBan board and SCRUM like Sprint development cycles.
In Confluence everything important is documented, regarding how to develop an application for the Social Robot CMS. So read these docs carefully
and refer to it again during your development.
All three tools work together, so follow the instructions in this guide carefully!

### Versioning
Each application for the Social Robot CMS has two different versions, the one you use for active development and one release version that is ready to
publish it.
The user never sees your development version. It is only for you, developing and testing your application.
The release is a already tested version of your development. It generates no error during common usage. It can be installed and managed through the Social Robot CMS.
Also, the installation through the Social Robot CMS and the interaction with robot, even if the robot has malfunctions, was already tested.
To identify your application changes for your Android application, the release version also get an Android specific versioning system. Therefore, you
have to set two values in your apps build.gradle:

    defaultConfig {
        ...
        versionCode 2
        versionName "1.1"
        ...
    }

versionCode is an increasing natural number. For every release this number increases by one.
versionName is a human-readable name. The correct usage differs between projects. One some we use a global release versioning system.
But normally a common versioning is used (see https://en.wikipedia.org/wiki/Software_versioning)
Normally you cannot publish this version on your own. If you're development version is ready to publish, you ask the SCRUM master to publish it.
The SCRUM master here is also the product owner. He or she is managing the development, as well as the final application releases that are
published to the users.

#### Global project versioning
On some projects, where we use the Social Robot CMS, we provide a global versioning system. To identify applications developed for the SRCMS,
inside the projects lifecycle, the projects development itself has different versions. Normally they are seperated into different releases, for each month,
in each project year.

The default version name looks like this

YEAR.MONTH.RELEASE

Where you should replace

- YEAR by the year of the projects release
- MONTH by the month of projects release
- RELEASE by the number of the projects release in this month

For example: The version name of the second release of June in 2020 will look like this: 2020.06.02
So, if the project you are developing for, uses this global versioning system, you set the versionName from your applications build.gradle regarding the
pattern above. Otherwise, you use the common pattern.

## Workflow
Follow this workflow to create and publish a repository.

### General
For each development, enhancement, or fix, a separate task needs to be created in Jira for the project development workflow.
Therefore a Kanban board is used, together with a SCRUM like development organisation (like mentioned above).
For all projects, English is the default language! No other languages are allowed inside Jira or Bitbucket!

### Jira Kanban Board
So each project you are working in gets its own kanban board.
Also, the Kanban board contains not only task for one application, but for the whole project content, so for different applications and new features or
fixes for that application.
The Kanban board is not used for anything else, then the application development. Everything else to organize, has be done somewhere else.
Otherwise, like normal Kanban, it has some different columns, that can different in each project:

**Backlog**
As in SRCMS, used for a list of tasks, features or apps that are requested for development, but not in focus now. Take it as a Wishlist your
definitely want to work on.
Requests that are not usable, will not work or not relevant for the project, never appear in the workflow!

**Scheduled**
These tasks are scheduled for development. You should try to fulfill them within one of next sprints.
How long a sprint last, depends on your project.

**In Development**
Here are task you currently work on.
Sometimes development can be seperated into sub categories like normal development, fixes or enhancement (new features)
If you start working, take one task, drag it the development column and start working on it (see below)

**Technical Test**
Drag a task here, if you are testing anything you developed.
No need to do that for every single line of code. But if you think you did it, do a overall technical test here.
Also, unit test can be executed at this point.
If the test fails, drag the task back to development. It is maybe automatically placed in the regarding sub category for fixing some things (if
available)
Is the test succeeds, drag the task to the next step.
You don't want or can't continue working on this task. Maybe you want to do to anything else instead for the moment. Drag ist back to Scheduled.

**Integration Test**
Task here mit be used for an integration test.
That means you have to test, if they work on a robot, are installable through a SRCMS repository and the SRCMS core app.
Maybe here are other things need to be checked. For example, if the design rules are implemented correctly or anything else.

Therefore, you normally cannot exit this step by yourself.
The SCRUM master ist responsible to check a lot of things here. Normally not that the app is working together with the robot or any other
technical system.
But anything else, like building a release from your app.

Not all task must pass an integration test.
Maybe your actual task is only a small code change, like setting a new button color, Fixing some text typos or anything else that don't
belong to the robot or the app installation.
For these tasks, this step can be skipped.

If your integration test fails, your task normally gets a notice from the SCRUM master, why it failed.It than goes bag to the development step (maybe subcategroy fix).
You should work on fixing the issue and do again a technical test and put it back to the integration test.
If the integration test succeeds, the SCRUM master will drag it to next step, which normally is done.
Here you don't have to do anything else.

**Done**
Task here are ready to publish.
They have a stable code on a separate branch of you Bitbucket repository.

**Release**
Task here are completed and release.
There is nothing more to do with them.

**Denied**
Tasks here are denied after they were requested.
Sometimes a task was requested for development and is in the backlog, but is obsolete now.
For example the fix a bug, that after some research appears to be not a bug, but a user failure.

#### Creating tasks
When you create a new task, you were asked for different values:

- Issue Type: Select the type of your task.
- Summary: A brief summary what to do inside your task
- Component: Each application in a project gets its own component. Select the app your task is for. Now you can select active tasks by the app they belong to. If your app has no task, create a new one and always use this task for this specific app.
- Description: Add a more detailed description what to do. Maybe what design pattern should be implemented or a notice about errors that happened due to a bug you want to fix.
- Fix Version: This is the projects release version (if a global project versioning is used), you task should be published with.
- Priority: Select the priority of you task. Priorities helping you to focus and the important tasks.  The Highest priority is displayed using a separate swim lane on the Kanban board.
- Linked Issues: Select how this task is related to other task (see revision tasks, explained below)
- Assignee: You can select someone, that should do the task (normally this is used only by the SCRUM master).  Or you can click Assign me, to assign ourselves.  You can filter the actual tasks, that are assigned to you.

After you created a task, a popup appears.
Use it to directly open the task and request it. Otherwise, it will not appear in the backlog!

### Bitbucket Software Repository
Bitbucket is a Git software repository system. There should be projects for your projects applications.
Here normally you can create a own repository, or the SCRUM master creates one for you.

Inside your repository are only a few rules you must take care of:

**Commit always**
For each change of code, each new single functionality, commit the changes. Don't integrated different changes into one commit!
Else you cannot rollback single changes!

**Good comments**
Write a good comment description, that explains, what you have done.

**Use branches**
While it is good to use many branches, you are only forced to use a master (or main) branch, containing always a clean and stable release
version of you application and a development branch (mostly called dev), containing your actual work

**Push & Pull**
Always synchronize your work online.
Therefore, do a fetch/pull request on your project, to look for changes, before you start working.
And at the end of your work (also for a short or long break), push your branches. Also push a branch, if you are checkout another one.

Besides this, there are usefully hints to do with your branches, to easily track your changes:

**Synchronize Jira and Bitbucket**
For each task, create a new branch, using Jira.
Always use Jira to create the branch. Then the task and the branch are connected (otherwise they are not!)
Always use your development branch as source for the new branches.

**Use revision tasks**
For each revision you want to publish, create a new task, naming the Apps name and revision number (like MyApp rev. 3) and a new branch.
For each task you want to include into that revision, set the task as child of the revision task.

**You are done**
If you are done ith one task, merge it into the corresponding revision task:
If this succeeds the integration test, increase the apps version code number and set the version name.

Now merge the revision branch into your development branch.

At the end a revision task, including different changes from several tasks, must always pass the integration test.
The individuals task belonging to it, must not.

With this, your development branch contains always the revision, that are ready to publish.
While the master branch contains the revisions, that are published. With this you can create revisions, that are not published (that can
happen).

**Document**
Not only use the source code documentation (that is good coding style, you have to do).
Also use the Jira comment section and file attachment, to document changes, processes and things that happened during working on a task.
For example where you downloaded a picture, or found some library or tool you will use inside a task.

See Dev-Branches Steps.pdf form more information about the Git branches

## Optimization
To optimize the final release apps size, only include architectures of instruction sets, that are available on the final device.
Edit your applications build.gradle and add the following:

    defaultConfig {
        ...
        ndk{
            abiFilters 'armeabi-v7a', 'x86'
        }
        ...
    }

replace ```armabi-v7``` and ```x86``` with a list of supported ABIs of the target device.

For more see https://developer.android.com/ndk/guides/abis

### Pepper ABI
The Pepper uses the following ABIs:

- armeabi-v7a
- x86