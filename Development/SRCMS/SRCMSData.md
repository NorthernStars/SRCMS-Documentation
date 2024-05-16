# SRCMSData

The SRCMSData class is a representation of the data sent by SRCMS (SocialRobotCMS) via an intent to all called apps. This class encapsulates the data and provides methods for generating a JSON representation of the data.

## Properties

* `status` (String): Represents the status of the SRCMS data. Can be `null` if the value is not provided.
* `showingAppsCategory` (String): Represents the category of apps being shown in the SRCMS data. Can be `null` if the value is not provided.
* `preferences` (JSONObject): Represents additional preferences in the SRCMS data. Can be `null` if the value is not provided.

## Methods

#### toJSON

`fun toJSON(): JSONObject`

Generates a JSON representation of the SRCMSData object by creating a JSONObject and adding the data
properties to it. 

* Returns:
	* Generated `JSONObject`

## Companion Object

The companion object contains utility methods for creating `SRCMSData` objects from JSON.

#### fromJSON

`fun fromJSON(string: String): SRCMSData`

Static function that creates an SRCMSData object from a JSON string representation. The
JSON string is converted to a JSONObject, and the required keys are extracted to construct the `SRCMSData`.

* Parameters:
	* `string`: `JSON` string containing the data to convert to a `SRCMSData` object.
* Returns
	* `SRCMSData`: Object created from string.
