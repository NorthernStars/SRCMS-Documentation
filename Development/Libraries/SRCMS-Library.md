# SRCMS-Library

The SRCMS-Lib is designed to help you within your app to interact with the SRCMS.

## Installation

This requires you to use the Android Studio. For this follow these step to install the srcms-lib:

1. Clone the git maven repository from https://bitbucket.iue.fh-kiel.de/projects/SRC/repos/srcms-lib-maven/ to your local maven repository
location:

	a. Windows: `C:\Users\<username>\.m2`<br>
	b. Linux: `/home/<username>/.m2`<br>
	c. Mac: `/Users/<username>/.m2`

> **_NOTE:_** The git repository content must be copied into a sub-directory named repository!

2. Include the maven local repository:<br>
Add the mavenlocal() to your projects settings.gradle:
```
pluginManagement {
	repositories {
		mavenLocal()
	}
}
```

3. Include the srcms-lib into your project to be able to use it inside your apps build.gradle:
```
dependencies {
	implementation 'de.fhkiel.srcms.lib:srcmslib:x.x.x'
}
```
Replace the x.x.x with the latest version of the SRCMS Library inside your Maven Repository.

4. Install the Robot SDKs

	a. Install Android Studio plugins:<br>
	https://developer.softbankrobotics.com/pepper-qisdk/getting-started/installing-pepper-sdk-plug <br>

	b. Create a robot application:<br>
	[English version (see Step 2)](https://qisdk.softbankrobotics.com/sdk/doc/pepper-sdk/ch1_gettingstarted/starting_project.html#id1) <br>
	[German version](https://confluence.iue.fh-kiel.de/display/IuERL/Pepper#Pepper-ProblememitdemProjekt-SetupimAndroidStudio(qiSDK))


## Classes

The SRCMS-Lib includes several classes to handle different things inside the SRCMS world. Here is only a short description of the, refer to the
generated JavaDoc for further information.

| Object   |    Description |
|-----------|---------------|
|SRCMSActivity | A basic RobotActivity class to extend to use for an robot application. Hdandles the basic usage of the robots functions. |
|SRCMSAppCategroy | A category representing an apps category inside the SRCMS world. |
|SRCMSAppInfo | An class to store information about an app for the SRCMS at a online repository. |
|SRCMSAppIntent | Class to handle the information, the SRCMS uses as extras data in an Androids intent when calling an SRCMS app. |
|SRCMSDownloadHelper | Class with static function to download files. |
|SRCMSFragment | A Fragment class used to extend. Includes some basic functions to show Toast massages and navigate to another fragment using Actions. |


## Content Manager

Include the navigation graph of the srcms-lib in your app navigation graph:

```
<navigation ...>
    <include app:graph="@navigation/nav_graph_content_manager" />
</navigation>
```

In your fragment where you want to navigate to the content manager, add the deep link request to your navigate() -call:

`findNavController().navigate(FragmentContentManager.getRequest())`


## SRCMSActivity

## SRCMSDownloadHelper

The SRCMSDownloadHelper provides functions to handle web directory listings, file downloads, and file unzipping.

Supported files: 
The SRCMSDownloadHelper class has static function to use for handling file downloads.
The class can download different fileteypes which are (since version 0.0.9): 

* jpg
* png
* gif
* svg
* mp3
* ogg
* apk
* zip

The class can also handle the unzipping of zip files into a directory.

### Classes

#### SRCMSDownloadHelper

The _SRCMSDownloadHelper_ class provides static functions to handle web directory listings, file
downloads, and file unzipping.

#### _Functions_
**isDirectory**

`fun isDirectory(url: URL): Boolean`

This function determines whether a given URL represents a directory or not.

* Parameters:
	* `url`: The URL to check.
* Returns:
	* `true` if the URL represents a directory, `false` otherwise.

**getDirectoryListing**

`fun getDirectoryListing(url: URL): MutableList<URL>` 

This function retrieves a list of URLs available through an Apache server's directory listing. It queries for
HTML `<li>` tags followed by an `<a>` tag with an 'href' attribute.

* Parameters:
	* `url`: The URL to read the directory data from.
* Returns:
	* A mutable list of URLs available on the site

**getDirectoryListing**

`fun getDirectoryListing(url: URL, fileEnding: String?): MutableList<URL>`

This overloaded function retrieves a list of URLs available through an Apache server's directory listing,
filtered by a specified file ending. It queries for HTML `<li>` tags followed by an `<a>` tag with an 'href'
attribute.

* Parameters:
	* `url`: The URL to read the directory data from.
	* `fileEnding`: The file ending to filter the directory listing. Pass `null` to get all URLs.
* Returns:
	* A mutable list of URLs available on the site, filtered by the specified file ending.


**deleteFile**

`fun deleteFile(file: File): Boolean`

This function deletes a file.

* Parameters:
	* `file`: The file to delete.
* Returns:
	* `true` if the file is deleted successfully, `false` otherwise.


**download**

`fun download(downloadURL: URL, downloadLocation: File,
suffix: String = ""): File?`

This function downloads a file and saves it to the specified location.

* Parameters:
	* `downloadURL`: The URL of the file to download.
	* `downloadLocation`: The path where the file should be downloaded. It can be a directory to create a temporary file or a concrete file.
	* `suffix`: The file suffix to be appended when creating a temporary file. Default is an empty string.
* Returns:
	* A `File` object pointing to the downloaded file if the download is successful, `null` otherwise.


**downloadJPG**

`fun downloadJPG(downloadURL: URL, downloadLocation: File): File?`

This function is a specialization of the download function for downloading JPG files.

* Parameters:
	* `downloadURL`: The URL of the JPG file to download.
	* `downloadLocation`: The path where the file should be downloaded. It can be a directory to create a temporary file or a concrete file.
* Returns:
	* A `File` object pointing to the downloaded JPG file if the download is successful, `null` otherwise.


**downloadPNG**

`fun downloadPNG(downloadURL: URL, downloadLocation: File): File?`

This function is a specialization of the download function for downloading PNG files.

* Parameters:
	* `downloadURL`: The URL of the PNG file to download.
	* `downloadLocation`: The path where the file should be downloaded. It can be a directory to create a temporary file or a concrete file.
* Returns:
	* A `File` object pointing to the downloaded PNG file if the download is successful, `null` otherwise.


**downloadGIF**

`fun downloadGIF(downloadURL: URL, downloadLocation: File): File?`

This function is a specialization of the download function for downloading GIF files.

* Parameters:
	* `downloadURL`: The URL of the GIF file to download.
	* `downloadLocation`: The path where the file should be downloaded. It can be a directory to create a temporary file or a concrete file.
* Returns: 
	* A `File` object pointing to the downloaded GIF file if the download is successful, `null` otherwise.


**downloadSVG**

`fun downloadSVG(downloadURL: URL, downloadLocation: File): File?`

This function is a specialization of the download function for downloading SVG files.

* Parameters:
	* `downloadURL`: The URL of the SVG file to download.
	* `downloadLocation`: The path where the file should be downloaded. It can be a directory to create a temporary file or a concrete file.
* Returns:
	* A `File` object pointing to the downloaded SVG file if the download is successful, `null` otherwise.


**downloadMP3**

`fun downloadMP3(downloadURL: URL, downloadLocation: File): File?`

This function is a specialization of the download function for downloading MP3 files.

* Parameters:
	* `downloadURL`: The URL of the MP3 file to download.
	* `downloadLocation`: The path where the file should be downloaded. It can be a directory to create a temporary file or a concrete file.
* Returns:
	* A `File` object pointing to the downloaded MP3 file if the download is successful, `null` otherwise.


**downloadOGG**

`fun downloadOGG(downloadURL: URL, downloadLocation: File): File?`

This function is a specialization of the download function for downloading OGG files.

* Parameters:
	* `downloadURL`: The URL of the OGG file to download.
	* `downloadLocation`: The path where the file should be downloaded. It can be a directory to create a temporary file or a concrete file.
* Returns:
	* A `File` object pointing to the downloaded OGG file if the download is successful, `null` otherwise.


**downloadAPK**

`fun downloadAPK(downloadURL: URL, downloadLocation: File): File?`

This function is a specialization of the download function for downloading APK files.

* Parameters:
	* `downloadURL`: The URL of the APK file to download.
	* `downloadLocation`: The path where the file should be downloaded. It can be a directory to create a temporary file or a concrete file.
* Returns:
	* A `File` object pointing to the downloaded APK file if the download is successful, `null` otherwise.


**downloadZIP**

`fun downloadZIP(downloadURL: URL, downloadLocation: File): File?`

This function is a specialization of the download function for downloading ZIP files.

* Parameters:
	* `downloadURL`: The URL of the ZIP file to download.
	* `downloadLocation`: The path where the file should be downloaded. It can be a directory to create a temporary file or a concrete file.
* Returns:
	* A `File` object pointing to the downloaded ZIP file if the download is successful, `null` otherwise.


**unzip**

`fun unzip(zipFile: File, destinationDirectory: File): Boolean`

This function extracts the contents of a ZIP file to a specified destination directory.

* Parameters:
	* `zipFile`: The ZIP file to be extracted. It must be readable.
	* `destinationDirectory`: The directory where the contents of the ZIP file will be extracted. It must be writable.
* Returns:
	* `true` if the ZIP file is successfully extracted, `false` otherwise.


**unzip**

`fun unzip(sourceFile: File, destinationDirectory: File, password: String?): Boolean`

This function extracts the contents of a ZIP file to a specified destination directory, with the option to provide a password for encrypted ZIP files.

* Parameters:
	* `sourceFile`: The ZIP file to be extracted. It must be readable.
	* `destinationDirectory`: The directory where the contents of the ZIP file will be extracted. It must be writable.
	* `password`: The password for the ZIP file, if it is encrypted. Set to `null` if no password is required.
* Returns:
	* `true` if the ZIP file is successfully extracted, `false` otherwise.

### Code Snippets

#### Explanation

This function downloads and unzips files from a given URL to a destination directory. It performs the following steps:

1. The `getDirectoryListing` function from the `SRCMSDownloadHelper` class is called with the `url` parameter and a file ending filter of "`.zip`". This retrieves the list of available files from the specified URL, limited to files with a ZIP file extension.
2. The function iterates through each file URL obtained from the `fileList`.
3. For each file URL, the function attempts to download the file using the `download` function from the `SRCMSDownloadHelper` class. If the download is successful, a `File` object representing the downloaded file is returned. If the download fails or the file is not a ZIP file, the function skips to the next iteration using the `continue` statement.
4. If the download is successful, the function proceeds to unzip the downloaded file using the `unzip` function from the `SRCMSDownloadHelper` class. The contents of the ZIP file are extracted to the `destinationDirectory`.
5. After successful extraction, the function deletes the downloaded file to clean up the temporary storage.
6. If any unzipping operation fails, the function returns `false` to indicate that not all files were successfully downloaded and unzipped.<br>
Otherwise, it returns `true` to signify that all files have been successfully processed.

#### Kotlin

```
import java.io.File
import java.net.URL
/**
 * Downloads and unzips files from a given URL to a destination directory.
 *
 * @param url The URL from which the files will be fetched.
 * @param downloadLocation The path where the files should be downloaded. Can be a directory to create temporary files or concrete files.
 * @param destinationDirectory The directory where the contents of each downloaded file will be extracted.
 * @return True if all files were successfully downloaded and unzipped, false otherwise.
 */
fun downloadAndUnzipFilesFromURL(url: URL, downloadLocation: File, destinationDirectory: File): Boolean {
    // Get the list of available files from the URL
    val fileList = SRCMSDownloadHelper.getDirectoryListing(url, ".zip")
    // Iterate through the remote files
    for (fileURL in fileList) {
        // Download the file
        val downloadedFile = SRCMSDownloadHelper.download(fileURL, downloadLocation) ?: continue
        // Unzip the file
        val success = SRCMSDownloadHelper.unzip(downloadedFile, destinationDirectory)
        // Clean up the downloaded file
        downloadedFile.delete()
        // If unzipping fails, return false
        if (!success) {
            return false
        }
    }
    return true
}
```

#### Java

```
import java.io.File;
import java.net.URL;
import java.util.List;
/**
 * Downloads and unzips files from a given URL to a destination directory.
 *
 * @param url                  The URL from which the files will be fetched.
 * @param downloadLocation     The path where the files should be downloaded. Can be a directory to create temporary files or concrete files.
 * @param destinationDirectory The directory where the contents of each downloaded file will be extracted.
 * @return True if all files were successfully downloaded and unzipped, false otherwise.
 */
public static boolean downloadAndUnzipFilesFromURL(URL url, File downloadLocation, File destinationDirectory) {
    try {
        // Get the list of available files from the URL
        List<URL> fileList = SRCMSDownloadHelper.getDirectoryListing(url, ".zip");
        // Iterate through the remote files
        for (URL fileURL : fileList) {
            // Download the file
            File downloadedFile = SRCMSDownloadHelper.download(fileURL, downloadLocation);
            if (downloadedFile == null) {
                continue;
            }
            // Unzip the file
            boolean success = SRCMSDownloadHelper.unzip(downloadedFile, destinationDirectory);
            // Clean up the downloaded file
            downloadedFile.delete();
            // If unzipping fails, return false
            if (!success) {
                return false;
            }
        }
        return true;
    } catch (Exception e) {
        e.printStackTrace();
        return false;
    }
}
```


## SRCMS Quiz-Module
Package: `de.fhkiel.srcms.lib.quizmodule`

### Classes

#### Quiz &lt;A, B&gt;

The `Quiz` class in the `de.fhkiel.srcms.lib.quizmodule` package is designed to organize a quiz.
It manages different sets of questions, with each set having a specific question type (Q) and answer type (A).

The `Quiz` class is defined with two generic type parameters, `Q` and `A`, representing the question and answer types, respectively.

#### _Properties_

* `questionsSets`: A mutable map (`MutableMap`) that stores the question sets. The keys are strings representing the names of the question sets, and the values are instances of the `QuestionSet` class with question type `Q` and answer type `A`.
* `excludedQuestionSets`: Another mutable map (`MutableMap`) that stores question sets that have been excluded. Similar to `questionsSets`, it uses string names as keys and `QuestionSet` instances as values. 

#### _Functions_

**addQuestionSet**

`addQuestionSet(questionSet: QuestionSet<Q, A>): Quiz<Q, A>`

This method adds a `QuestionSet` to the quiz.

* Parameters:
	* `questionSet`: The `QuestionSet` object to be added.
* Returns: 
	* The current `Quiz` object.


**getAvailableQuestionSetNames**

`getAvailableQuestionSetNames(): Set<String>`

This method retrieves the names of the available question sets.

* Returns: 
	* A set (`Set`) of strings representing the names of the available question sets.


**getQuestionSet**

`getQuestionSet(name: String, exclude: Boolean = false): QuestionSet<Q, A>?`

This method retrieves a specific `QuestionSet` based on its name. It also provides an option to exclude the set from the list of available question sets.

* Parameters:
	* `name`: The name of the `QuestionSet` to retrieve.
	* `exclude` (optional): A boolean value indicating whether to exclude the set from the available question sets. Defaults to `false`.
* Returns: 
	* The requested `QuestionSet` object, or `null` if no set with the given name is found.


**removeQuestionsSet**

`removeQuestionsSet(name: String): QuestionSet<Q, A>?`

This method removes a question set from the quiz based on its name.

* Parameters:
	* `name`: The name of the `QuestionSet` to remove.
* Returns: 
	* The removed `QuestionSet` object, or `null` if no set with the given name was found.


**getRandomQuestionSet**

`getRandomQuestionSet(): QuestionSet<Q, A>?` 

This method retrieves a random `QuestionSet` from the available question sets. It also removes the chosen set from the list of available sets.

* Returns: 
	* The chosen `QuestionSet` object, or `null` if there are no available sets.

#### _Usage_

To use the Quiz class, create an instance of it with appropriate question and answer types, and then utilize the available methods to manage the quiz and its question sets.

```
import de.fhkiel.srcms.lib.quizmodule.Quiz
import de.fhkiel.srcms.lib.quizmodule.QuestionSet

fun main() {
    // Create a Quiz object with Question type as String and Answer type as Int 
    val quiz = Quiz<String, Int>()
    
    // Create QuestionSets 
    val questionSet1 = QuestionSet<String, Int> ("Set 1")
    val questionSet2 = QuestionSet<String, Int> ("Set 2")
    
    // Add QuestionSets to the Quiz 
    quiz.addQuestionSet(questionSet1)
    quiz.addQuestionSet(questionSet2)

    // Get available QuestionSet names 
    val availableSetNames = quiz.getAvailableQuestionSetNames()
    println("AvailableQuestionSets: $availableSetNames")
    
    // Get a specific QuestionSet
    val selectedQuestionSet = quiz.getQuestionSet("Set 1")
    println("SelectedQuestionSet: $selectedQuestionSet")
    
    // Remove a QuestionSet
    quiz.removeQuestionsSet("Set2")
    println("QuestionSet 'Set 2'removed")

    // Get a random QuestionSet
    val randomQuestio nSet = quiz.getRandomQuesionSet()
    println("RandomQuestionSet: $randomQuestionSet")
}

```

In this example, we create a `Quiz` object with question type `String` and answer type `Int`. We then add two `QuestionSet` objects to the quiz using the `addQuestionSet` function. We retrieve the available QuestionSet names using the `getAvailableQuestionSetNames` function and print them. 

Next, we get a specific QuestionSet using the `getQuestionSet` function by providing the name "Set 1". We remove "Set 2" using the `removeQuestionsSet` function. Finally, we get a random QuestionSet using the `getRandomQuestionSet` function and print the result.

#### _Output_

```
Available QuestionSets: [Set 1, Set 2]
Selected QuestionSet: QuestionSet (name=Set 1, questions=[])
QuestionSet 'Set 2' removed
Random QuestionSet: null
```

#### Question &lt;Q, A&gt;

The `Question` class in the `de.fhkiel.srcms.lib.quizmodule` package represents a question and
its corresponding answers. It allows retrieval of the correct answer based on a specific attribute name.

The `Question` class is defined with two generic type parameters, `Q` and `A`, representing the question
type and answer type, respectively.

#### _Properties_

* `id`: An integer representing the ID of the question.
* `question`: An object of type `Q` representing the question.
* `answers`: A list of objects of type `A` representing the available answers for the question

#### _Functions_

**getCorrectAnswer**

`getCorrectAnswer(attributeName: String): A?`

This method retrieves the first correct answer from the list of answers based on a specified attribute
name. It checks if any object in the answers list of type `A` has a property with a name matching the
provided attribute name.

* Parameters:
	* `attributeName`: The name of the attribute to look for in the answer objects.
* Returns: 
	* The correct answer of type `A`, or `null` if no correct answer was found.


**toString**

`toString(): String`

This method overrides the default `toString()` method to provide a string representation of the question
and its answers. It formats the output as follows:

```
<question> (<number of answers>):
    <answer1>
    <answer2>
    ...
```

* Returns: 
	* A string representation of the question and its answers.

#### _Companion Object_

`DEFAULT_CORRECT_ANSWER_ATTRIBUTE`

A constant string representing the default attribute name used to identify the correct answer. Its value is
set to "correct".

#### _Usage_

To use the `Question` class, create an instance of it with appropriate question and answer types, and then utilize the available methods to retrieve the correct answer and represent the
question as a string.

```
import de.fhkiel.srcms.lib.quizmodule.Question

data class Answer(val option: String, val correct: Boolean)

fun main() { 
    // Create a Question with Int type question and Answer type as Answer class
    val question = Question<Int, Answer>(1, 42, listOf(Answer("Option A", true), Answer("Option B", false), Answer("Option C", false)))
    
    // Get the correct answer using the default attribute name
    val defaultCorrectAnswer = question.getCorrectAnswer(Question.DEFAULT_CORRECT_ANSWER_ATTRIBUTE)
    println("DefaultCorrectAnswer: $defaultCorrectAnswer")

    // Get the correct answer using a custom attribute name
    val customCorrectAnswer = question.getCorrectAnswer("correct")
    println("CustomCorrectAnswer: $customCorrectAnswer") 
    
    // Print the question details
    println(question)
}
```

In this example, we create a `Question` object with an `Int` type question and a list of `Answer` objects. Each `Answer` object has an `option` and a `correct` property indicating whether it is the
correct answer.

We create a sample question with the number 42 as the question and three answer options. We then use the `getCorrectAnswer` function to retrieve the correct answer based on the default
attribute name "correct" and a custom attribute name. We print both the default correct answer and the custom correct answer.

Finally, we print the question details using the `toString` function, which provides the question text, the number of answers, and each answer option.

#### _Output_

```
Default Correct Answer: Answer(option=Option A, correct=true)
Custom Correct Answer: Answer(option=Option A, correct=true)
42 (3): Answer(option=Option A, correct=true)
        Answer(option=Option B, correct=false)
        Answer(option=Option C, correct=false)
```

#### QuestionSet &lt;Q, A&gt;

The QuestionSet class in the de.fhkiel.srcms.lib.quizmodule package is used to store multiple questions and their corresponding answers. It provides methods to retrieve questions, generate
random questions, and parse data from JSON format.

The QuestionSet class is defined with two generic type parameters, Q and A, representing the question type and answer type, respectively.

#### _Properties_

* `name`: A string representing the name of the question set.
* `questions`: A map of questions with integer IDs (`Int`) as keys and objects of type `Q` as values.
* `answers`: A map of answers with question IDs (`Int`) as keys and lists of objects of type `A` as values.
* `size`: An integer representing the number of questions in the question set.

#### _Functions_

**getAll**

`getAll(): Map<Int, Question<Q, A>>`

This method returns a map of all questions in the question set, where the question ID (`Int`) is used as
the key and the corresponding `Question` object is the value.

* Returns: 
	* A map of all questions in the question set.


**getQuestion**

`getQuestion(id: Int): Question<Q, A>?`

This method retrieves a specific question from the question set based on its ID.

* Parameters:
	* `id`: The ID of the question to retrieve.
* Returns: 
	* The `Question` object with the specified ID, or `null` if no question was found.


**getRandomQuestion**

`getRandomQuestion(): Question<Q, A>?`

This method returns a random question from the question set.

* Returns: 
	* A random `Question` object, or `null` if the question set is empty.


**getRandomQuestion**

`getRandomQuestion(exclude: List<Int>?): Question<Q, A>?`

This method returns a random question from the question set, excluding the questions specified in the `exclude` list.

* Parameters:
	* `exclude`: A list of question IDs (`Int`) to exclude from the available options.
* Returns: 
	* A random `Question` object, or `null` if no suitable question is available.


**toString**

`toString(): String`

This method overrides the default `toString()` method to provide a string representation of the question
set. It includes the name of the question set and lists all the questions and their details.

* Returns: 
	* A string representation of the question set.


#### _Companion Object_

The `QuestionSet` class includes a companion object that provides additional functionality.

**fromJSON**

`fromJSON(...)`

This function creates a `QuestionSet` object from JSON arrays containing question and answer data. It parses the JSON arrays and maps the question and answer data to the appropriate formats.

* Parameters:
	* `jsonArrayQuestions`: A `JSONArray` containing question data.
	* `jsonArrayAnswers`: A `JSONArray` containing answer data.
	* `name`: The name of the question set.
	* `keyID`: The key used to identify the question ID in the JSON objects. Default: "id".
	* `keyQuestion`: The key used to identify the question in the JSON objects. Default: "question".
	* `keyAnswer`: The key used to identify the answer in the JSON objects. Default: "answer".
	* `keyCorrectAnswer`: The key used to identify the correct answer in the JSON objects. Default: "correct".
* Returns: 
	* A `QuestionSet` object with questions and answers parsed from the provided JSONarrays.

**fromSimpleJSONStrings**

`fromSimpleJSONStrings(...)`

This function creates a `QuestionSet` object from a JSON array containing simple question and answer
strings. It assumes that each JSON object in the array contains question and answer data.


#### CSVParser

The `CSVParser` class in the `de.fhkiel.srcms.lib.quizmodule` package provides static functions to parse data for `QuestionSet` objects from CSV files.

The `CSVParser` class contains companion object functions for parsing CSV data into JSON format.

#### _Companion Object_

The `CSVParser` class includes a companion object that provides the following functionality:

**toJSON**

`toJSON(...)`

This private function reads CSV table data from an `InputStream` and converts it into a `JSONArray` of `JSONObjects`.

* Parameters:
	* `inputStream`: The `InputStream` to read the CSV data from.
	* `useFirstLineAsHeader`: A boolean indicating whether to use the first line as the table header. Default: `true`.
			* `defaultHeaderString`: The header string to use if `useFirstLineAsHeader` is `false`. Default: "`$DEFAULT_ID_ATTRIBUTE`;`question`;`answer`".
	* `delimiterChar`: The character used as the delimiter to separate columns in the CSVtable. Default: ';'.
	* `addID`: A boolean indicating whether to automatically add an ID attribute to the JSONobjects. Default: `false`.
	* `idAttribute`: The key name of the ID attribute, used if `addID` is `true`. Default: "`id`".
	* `idStartValue`: The start value for automatically increasing the ID parameter, used if `addID` is `true`. Default: `1`.
* Returns: 
	* A `JSONArray` of `JSONObjects` containing the parsed CSV table data.


**getJSONFromCSV**

`getJSONFromCSV(fileName: String): JSONArray`

This function retrieves a `JSONArray` of `JSONObjects` from a CSV file specified by its name.

* Parameters:
	* `fileName`: The name of the file to read the CSV table from.
* Returns: 
	* A `JSONArray` of `JSONObjects` containing the parsed CSV table data.


**getJSONFromCSV**

`getJSONFromCSV(...)`

This function retrieves a `JSONArray` of `JSONObjects` from a CSV file.

* Parameters:
	* `file`: The `File` object representing the CSV file to read.
	* `addID`: A boolean indicating whether to automatically add an ID attribute to the JSON objects. Default: `true`.
	* `idAttribute`: The key name of the ID attribute, used if `addID` is `true`. Default: "`id`".
	* `idStartValue`: The start value for automatically increasing the ID parameter, used if `addID` is `true`. Default: `1`.
* Returns: 
	* A `JSONArray` of `JSONObjects` containing the parsed CSV table data.

### Code Snippets

**Default Values**

| Value | Default |
|-----|-----|
|column name ID | id |
column name question | question |
column name answer | answer |
column name correct answer | correct |
data in column correct answer if answer is correct | not empty |
default first id number | 1 |
default delmiter char | ; |

```
// read questions file to [JSONArray]
val jsonArrayQuestions = CSVParser.getJSONFromCSV(file = fileQuestions)
```
```
// read answers file to [JSONArray]
val jsonArrayAnswers = CSVParser.getJSONFromCSV(file = fileAnswers)
```
```
// read questions and answers from ONE file to [JSONArray]
val jsonArrayQuestionsAndAnswers = CSVParser.getJSONFromCSV(file = fileQuestionsAnswers)
```
```
// create from question and answer file [QuestionSet]
val questionSet = QuestionSet.fromJSON(
	jsonArrayQuestions = jsonArrayQuestions,
	jsonArrayAnswers = jsonArrayAnswers,
	name = name
)
```
```
// create from question and answer ONE file [QuestionSet]
val questionSet = QuestionSet.fromJSON(
    jsonArray = jsonArrayQuestionsAndAnswers,
    name = name
)
```

### Testing

You can test the library's functions with the test class `QuestionSetTest` from test package.

In the code provided, the companion object contains several values that serve as configuration
parameters for the program. These values are typically static and accessible without an instance of the
class. Let's explore each value and its purpose:

1. `CSV_FILE_PATH`: This value represents the file path of the CSV data to be parsed. It specifies
the location of the CSV file on the file system.
2. `CSV_SEPARATOR`: It defines the separator character used in the CSV file to separate different
values or fields. Common separators include commas, tabs, or semicolons.
3. `QUESTION_COUNT`: This value determines the number of questions to be generated in the
question set. It specifies how many questions the program should include in the generated
output.
4. `ANSWER_COUNT_MIN`: It represents the minimum number of answers to generate for each
question in the question set. This value helps control the variability of the generated data.
5. `ANSWER_COUNT_MAX`: This value specifies the maximum number of answers to generate for
each question in the question set. It provides an upper limit for the number of answers.
6. `RANDOM_OPTION_COUNT`: It defines the number of random options to be generated for each
question. Random options are used to diversify the available choices in the question set.
7. `TEMP_FILE_PREFIX`: This value represents the prefix for temporary file names created during
testing. It helps identify and manage temporary files generated during the program's execution.

These values in the companion object allow for easy customization and adaptation of the program's
behavior. By modifying these values, users can adjust the program to their specific needs, such as
changing the source data file, controlling the number of questions or answers, and managing temporary
file names.

#### _Functions_

1. `parseSimpleCSVDataWithoutIDKey()`: Parses CSV data without an ID key, generates a simple question set, and tests it.
2. `parseSimpleCSVDataWithIDKey()`: Parses CSV data with an ID key, generates a simple question set, and tests it.
3. `parseCSVDataWithIDKey()`: Parses CSV data with an ID key, generates a question set with multiple answers, and tests it.
4. `getRandomOption()`: Generates a random question set, selects random questions, and checks for duplicates.
5. `getRandomOptionExclude()`: Generates a random question set, selects random questions excluding already selected ones, and checks for duplicates.
6. `generateCSVTestData()`: Generates test data for CSV files based on provided parameters.
7. `generateCSVTestFile()`: Generates a CSV test file with a given header and data.
8. `generateSimpleQuestionSet()`: Generates a simple question set with string-based questions and answers from CSV data.
9. `generateQuestionSet()`: Generates a question set with string-based questions and multiple answers from CSV data.
10. `testOptionSet()`: Generates and tests question sets with randomly generated values, ranges, and names.
11. `deleteTempFiles()`: Deletes temporary files created during testing.
