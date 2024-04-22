# Logging Service

## Description

The SRCMS Logging Service is a local RESTful api webservice to send logging messages to. The services takes care about the correct storage of the
log files.

To access the service POST and GET request had to be made to a specific IP inside the local network, the robot is using. To do that, there are two
option:

1. <del>Use the SRCMS-Library that contains classes and functions to handle accessing the remote RESTful api. It is mainly developed for Kotlin
and Java applications.</del>
2. Implement your own POST and GET request, following this documentation

Hint: All POST requests include string data values using multiform-data.

Hint: On invalid request data, the logging service returns nothing. Only on using invalid requests or request types, errors are returned.
The logging service project can be found here:

https://bitbucket.iue.fh-kiel.de/projects/SRC/repos/srcms-logging-service

### Logging Types

The SRCMS Logging Service log differnt types of data.

* Service Data
* App Data

The Services handles settings the basic JSON loggig object, containing the name of the service or app, as well as the timestamp. But it logs any
content to the data value. Therefor any data is written as String into the data value of the logging object.
The sender, that is sending data to the loggin service, has to take care, that the logged data follows the documentation guidelines.

## Authentification
The logging service accepts only log messages from some registered applications (see Authetification below). Application that are not registered can
not send data to the logging service.

For sending data to the logging service a registered application has to login itself at the logging service using its name and a login key, that is
generated from the uid and key values registered with this application at the logging service.

After the application is loged in successfully, it recieves a session key, that is used for all further data logging requests. The session exires after a
certain time without logging activity of this application. If the session expired, the logging services will no longer respond to request using an expired
session key, the application than has to login again and use a new generated session key

## GET & POST Requests

Request to the logging service can be done, using GET and POST http requests. While no SSL certificate is applied until now, this service should not
be exposed to the web!

Both GET and POST request return string data (GET) or an status string (POST), which is "OK" if the post was usccessfull, or no data if it was not.

* The GET requests contain only one part:
The request url contains to url-path for what data is adressed. GET requests return only simple data
* POST request contain two parts:
The request url, in the same meaning as in GET request, about who wants to post what kind of data.
The request body. A simple string, that contains a simple json object, that contains the reuired data.

### Generating Application UID and Key (GET)

For registration of an application to the logging service a uid and a key is required. To let the loggin service generate valid keys, the followig GET
requests can be used:

`/generate/uid`

generates a valid application uid, while

`/generate/key`

generates a valid application key.
Be aware, that both values are of type _String_!

### Login Key
To login an application it needs a login key that is build using the generated application uid and key (See above) the following way:

1. Hash the application uid using a SHA-512 algorithm
2. Hash the application key using a SHA-512 algorithm
3. As _login key_ use the hashed ui, immediately followed by the hased application key.

Be aware that the resulting login key is of type String!

### Login Application (POST)
The request application login ´, to start a session, a POST request has to be done to:

`/app/login/{name}`

* where _name_ is the name of the application that wants to login.

The request has to use the login key value as string formatted json object like this

`{
  'key': '<KEY>'
}`

* `<KEY>`: the applications login key as string.

If the login was successfull, a session key is returned, that is used for all further request during the session is valid.
If the application was not able to login, nothing is returned.

### Log Service and App Data

Data of services described in this documentation are logged as service data.<br>
Data of end-user apps are logged as app data.

Both service and app data are POST request with the follwoing string formatted json object:

```
{
  'key': '<SESSIONKEY>',
  'data': '<DATA>'
}
```

* `<SESSIONKEY>`: Session key, generated at login, as string
* `<DATA>`: JSON String, stored inside data key in logging structure (see documentation), as string


#### Service Data

`/app/{name}/log/service/{service}`

where name is the applications name that wants to log data and service is the name of the service the logged data belongs to.

#### App 

`Data/app/{name}/log/app`

where name is the application name that want to log its individual data.