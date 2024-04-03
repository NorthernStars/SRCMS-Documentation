# Android-OS (DEPREACTED)
***This logging informations are deprecated and will not be used anymore!***

These services are logged regarding the operating system (Android ) specific data:

- Bluetooth
    - discovered-devices
    - BluetoothDevice
- WiFi
    - WifiInfo
    - ScanResult
- QR-Code
    - Raw-Data
---
## Bluetooth
---
Bluetooth data is logged in the following
syntax:

```
    {
        'name': String
        'enabled': Boolean
        'discovering': Boolean
        'state': Integer
        'bonded-devices': List<BluetoothDevice>
        'discovered-devices': List<JSONObject>
    }
```

- **name** user fraindly name of the bluetooth adapter
- **enabled** true if adapter is active, false otherwise.
- **discovering** true if adapter is currently discovering process, false otherwise
- **state** state of the bluetooth adapter, regarding android.bluetooth.BluetoothAdapter. It can be 2 for connecting, 1 for connection and 0 for disconnection
- **bonded-devices** list of bonded of bonded bluetooth devices
- **discovered-devices** list of discovered bluetooth devices

Only name, enabled and discovering are always available! Depending if there is a list of bonded or discovered devices, these attributes can be null, an
empty list or not available.
---

### discovered-devices
'discovered-devices' contains an list of json objects of the following data:

```
    {
        'device': BluetoothDevice
        'rssi': Integer
    }
```

- **device** BluetoothDevice object of the discovered device
- **rssi** the RSSI value for the remote device to discover distance to the device, 0 if no RSSI value is available

Be aware, that the list of discovered devices can change, while discovered devices are reported on one
timestamp, are not found on the next one and than are again found on the thrid one. This happens while
the system only reports when a device was discovered and the logging system has to collect a list of
devices and therefore will delete a device from this list after a timeout in that it was not discovered.

### BluetoothDevice
A bluetooth device represends a bluetooth device and contains following data:

```
    {
        'bond-state': Integer
        'address': String
        'name': String
        'type': Integer
    }
```

- **bond-state** bond state of the device reading android.bluetooth.BluetoothDevice
- **address** hardware address of this device. For example "00:11:22:AA:BB:CC"
- **name** user friendly name of the device
- **type** type of the device regarding android.bluetooth.BluetoothDevice. It can be a number from 0 to 3:

**Type:**
- **0** device unknown
- **1** device type: classic, for example: mobile phone
- **2** device type: dual mode, can be low energy and classic
- **3** device type: low energy, for example: headphone

---
## WiFi
---
Wifi data logged in the following syntax:

```
    {
        'enabled': Boolean
        'scan': Boolean
        'connectioninfo': List<WifiInfo>
        'scan-result': List<ScanResult>
    }
```

- **enabled** true if wifi is active, false otherwise.
- **scanning** true if wifi manager is searching for network, false otherwise
- **connectioninfo** returns a list of information about wifi connection state
- **scan-results** is a list of available wifi-networks
---
### WifiInfo
Represents the state of any Wi-Fi connection that is activ.

```
    {
        'SSID': String
        'IpAddress': Integer
        'rssi': Integer
        'link-speed' : Integer
        'state': Enum
    }
```

- **SSID** is a user-friendly name of a reachable Internet access
- **IpAddress** is an individual address that identifies a device on the Internet or on a local network. It ranges from 0.0.0.0 to 255.255.255.255. For example "192.158.1.38"
- **rssi** is the received signal strength indicator in dbm, 0 if no RSSI value is available. link-speed is the maximum speed at which devices can communicate with each other it is specified in bits per second. For example "100 Mbps"
- **state** represents information about the connection state. There are 6 different Types

State:
- Connected
- Connecting
- Disconnected
- Disconnecting
- Suspended
- Unknown

### ScanResult
Continuously, available Wi-Fi network will be found, if scanning is in process.

```
    {
        'SSID': String
        'rssi': Integer
    }
```

- **SSID** is a user-friendly name of a reachable Internet access
- **rssi** is the received signal strength indicator in dbm, 0 if no RSSI value is available.

---
## QR-Code

### Raw-Data
A QR-Code scanner returns the encapsulated result of decoding a barcode into an image.
the raw data contains:

```
    {
        'text' : String
        'rawbytes' : byte
        'numBits' : Integer
        'ResultPoint' : ResultPoints
        'format' : BarcodeFormat
        'Metadata' : Map<MetadataType, Object>
        'timestamp': long
    }
```

- **Text** returns the raw text encoded by the barcode rawbytes if it is applicable it returns bytes encoded by the barcode, otherwise it is 0
- **numBits** returns how many bits of rawbytes are valid. Usually it is 8 times its length
- **ResultPoint** returns the points related to the barcode in the image,. These are typicalle points identifying finder patterns or the corners of the barcode. The exact meaning is specific to the type of barcode that was decoded. It consists of x- and y- coordinates
- **format** represents the format of the barcode that was decoded. The QR-Code format is one out of seventeen possible formats.
- **Metadata** returns a mapping of keys to values. It contain optional metadata about what was detected about the barcode, for example: orientation. If nothing is detected it returns null.
