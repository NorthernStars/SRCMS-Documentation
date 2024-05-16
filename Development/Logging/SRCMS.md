# SRCMS

These services are logged regarding the SRCSM specific data:

---
## System Events
---
These system events are logged:

| Event | Data | Example | Description |
|-------|------|---------|-------------|
| START | <ul><li>Action</li></ul> | ```"action": "start"``` | System enters start phase. |
| UPDATE | <ul><li>Action</li></ul> | ```"action": "launch update"``` | System launches app update process. |
' APP LAUNCH | <ul><li>Action</li><li>SRCMSApp<sup>1</sup></li></ul> | ```"action": "launch app", app:"..."``` | App is started by user. |
| RESUME | <ul><li>Action</li><li>SRCMSApp<sup>1</sup></li></ul> | ```"action": "resumed", app:"..."``` | SRCMS resumes (from background), the app is the last started app. |

1: JSON representation of this object.