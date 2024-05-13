# Robot [DEPRECATED]
This logging informations are deprecated and will not be used anymore!

These services are logged regarding the robots specific data:

* Power
* The Power indicates the current battery status of the Robot.
* Awareness
	* Human
	* Head Frame
	* Age
	* Gender
	* Pleasure State
	* Excitement State
	* Engagement Intention State
	* Smile State
	* Attention State
* Sensors
	* touch-sensors
	* TouchState
* Animation
	* Exercise
	* Animationstate

## Power

The Power indicates the current battery status of
the Robot.
```
{
	'batteryPct' : float
}

```

* **batteryPct** returns the battery status in percent. It gives a value between 100 and 0.

## Awareness
The HumanAwareness function, of the robot, gives information about different characteristics of a
recognized human being 

### Human

The number reflects the count of recognized humans

```
{
	'human': Integer
}
```

Hint: the following characteristics are strongly dependent on incident light and therefor have a high
inaccuracy

### Head Frame
The Head Frame represents the location of  detected human.

```
{
	'Frame': Transform
}
```

Transform consists of two parameter, which provide information about translation and rotation of the
frame.

```
{
'Transform':
          {
        'Quaternion':{
	                    'x' : Double
	                    'y' : Double
	                    'z' : Double
	                    'w' : Double
                    },
        'Vector3':{
	                  'x' : Double
	                  'y' : Double
	                  'z' : Double
                  }
    }
}
```

* **Vector3** represents a 3D-Vektor, it is measured
* **Quaternion** represents the rotation

### Age
The age represents the estimated age a person
```
{
   'Age' : Integer
}
```
Be aware that age can also show a negative number, in that case the roboter is not able to estimate the
age.

### Gender

```
{
   'Gender' : Enum
}
```
The gender contains three different types:

* **male**
* **female**
* **unknown**

It is unknown if the robot is not able to observe a gender.

### Pleasure State
```
{
   'PleasureState' : Enum
}
```
The pleasure state contains four different types:

* **negative**
* **neutral**
* **positive**
* **unknown**

It is unknown if the robot is not able to observe a pleasure state.

### Excitement State
```
{
   'ExcitementState' : Enum
}
```
The excitement state contains three different types:

* **calm**
* **excited**
* **unknown**

It is unknown if the robot is not able to observe an excitement state.

### Engagement Intention State

```
{
   'EngagementIntentionState' : Enum
}
```
The engagement intention state contains four different types:

* **not interested**
* **interested**
* **seeking engagement**
* **unknown**

It is unknown if the robot is not able to observe an engagement intention state.

### Smile State
```
{
   'SmileState' : Enum
}
```
The smile state contains four different types:

* **not smiling**
* **smiling**
* **broadly smiling**
* **unknown**

It is unknown if the robot is not able to observe a smile state.

### Attention State
```
{
   'AttentionState' : Enum
}
```

The attention state contains ten different types:

* **looking at robot**
* **looking up**
* **looking down**
* **looking left**
* **looking right**
* **looking up left**
* **looking up right**
* **looking down left**
* **looking down right**
* **unknown**

It is unknown if the robot is not able to observe an attention state.

### Syntax

Awareness data logged in the following
syntax:
```
{
	'human': Integer
	'awareness':{
		'number':Integer
		'Age':Integer
		'Gender' : Enum
		'PleasureState' : Enum
		'ExcitementState' : Enum
		'EngagementIntentionState' : Enum
		'SmileState' : Enum
		'AttentionState' : Enum
	},
	'headFrame':{
		'rotation':{
			'x' : Double
		    'y' : Double
		    'z' : Double
		    'w' : Double
		},
		'3DVector': {                
	    	'x' : Double
	    	'y' : Double
		    'z' : Double
		},
	},
}
```

* **human** is the number of perceived humans.
* **awareness** returns all the listed items
* **headframe** returns the position of detected humans in coordinates

Everything is available, but can show unknown.

## Sensors

### touch-sensors
'**touch-sensors**' contains a list of json objects of the following data
```
{
	'name': String
	'state': TouchState
}
```

* **name** is the name of the sensor
* **state** is the TouchState object of the sensors touch state

### TouchState
The TouchState represents the sensors touch state and contains the following data:
```
{
	'last-changed': Long
	'touched': Boolean
}
```

* **last-changed** is the last times timestamp in nanoseconds, where the sensors state changed. If
no time is available this can be 0, or null.
* **touched** is true if the sensors is touched at the moment, false otherwise

Be aware, that the timestamp the touch changed last changed must NOT be the same, as the data was
logged. It is completely independent from that.

### Syntax

Robot sensors are logged in the following syntax:
```
{
	'touch-sensors': List<JSONObject>
}
```

* **touch-sensors** is a list of touch sensors of the robot. If robot has no touch sensors, the list can be null, empty or the attribute not available

## Animation
### Exercise
Exercise contain a list of Json object of the following data
```
{
	exercise: animationstate
}
```

### Animationstate
Animationstate refers to labels which have been added in a raw animation resource. It can be obtained
the named label with the corresponding timestamp.
```
{
	'animation': String
	'timestamp': long
}
```

* **animation**: is the name of the added label and can be any given String
* **timestamp** is the corresponding time in nanoseconds
