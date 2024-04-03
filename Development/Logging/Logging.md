# Logging
The SRCMS should be ablte to log several data in background in the future. The following data section are logged in general:

- Operating system specific data
- Robot specific data
- SRCMS specific data
- 
The detailed data, that is logged inside a asection. View the corresponding section documentation.

***Hint: This list is neither complete nor fixed. So during the project runtime, these logged services and data, as well as data structure can change!***

## Art of logging
The service data named above ist sored in individual files with a fixed file naming.

Every file is named by the service name, following a underscore _ and the current system timestamp in nanoseconds. Each file contains json formatted data following tis sytax for a json object:

```
    {
        'service': '<SERVICE-TYPE>'
        'timestamp': <TIMESTAMP-MILLISECONDS>
        'data': {
            <SERVICE-DATA>
        }
    }
```

    **<SERVICE-TYPE>** is the name of the service data is logged from. For example service: 'bluetooth'
    **<TIMESTAMP-NANOSECONDS>** is the timestamp in nanoseconds (type Long)
    **<SERVICE-DATA>** is the data logged for the service json object with key-value-pairs. Where the key specifies the data type and value the data itself.
    **<SERVIE-DATA>** The service data can be different for each service is not forced to consistent in all log files. Therefore the service data contains the logged data, assigned to a data-type specific key. The value of the data can then be any kind of object, regarding the data it represents.

For example a single user id can be logged inside the service data the following way:

```
    {
        'user-id': 7645638
    }
```

But it contain any kind of object. For example another object:

```
    {
        'users': {
            'logged-in': 7645638
            'active-profile': 90547856
        }
    }
```

Or a list of available WiFi networks:

    ```
    {
        'wifi-networks-available': [
            'wifi1',
            'wifi2',
            'eduroam',
            'NorthernStars'
        ]
    }
```

These examples are only this: Examples. So take a look at the service specific documentation for informations, how the data is store inside the log files.