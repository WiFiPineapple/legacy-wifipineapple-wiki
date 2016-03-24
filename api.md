# WiFi Pineapple Module API

## Introduction
Unlike the old web interface, the back end of the new interface has been decoupled from the front end. All requests to perform system actions are sent as POSTs to `/api/`. The content of the POST is JSON and contains a minimal of two parameters.
### The first parameter key must be either `system` or `module`
`system` is used for core system functions such as logging users in and performing system setup as well as managing notifications. `module` is used when sending a request to any of the default modules or to any user modules. The value is set to the module with which you are trying to communicate. For example, `"system": "notifications"` or `"module": "RandomRoll"`.
### The second parameter key `action`
This is set to the action you wish to perform. For instance, this could be `"action": "listNotifications"` or `"action": "getRandomRollRolls"`.
### Any other parameters are optional and are specific to the module and action you are requesting
Many actions do not require additional parameters. For instance, `{"system": "notifications", "action": "listNotifications"}` will return a list of all of the current unread notifications (as JSON). However, there are some functions, such as `addNotification`, that require additional parameters (in this case `message`). To create a new notifications, one would use the following request:
`{"system": "notifications", "action": "addNotification", "message": "Hello World!"}`
