# WiFi Pineapple Module API

## Introduction
Unlike the old web interface, the back end of the new interface has been decoupled from the front end. All requests to perform system actions are sent as POSTs to `/api/`. The content of the POST is JSON and contains a minimal of two parameters.
#### The first parameter key must be either `system` or `module`
`system` is used for core system functions such as logging users in and performing system setup as well as managing notifications. `module` is used when sending a request to any of the default modules or to any user modules. The value is set to the module with which you are trying to communicate. For example, `"system": "notifications"` or `"module": "RandomRoll"`.
#### The second parameter key `action`
This is set to the action you wish to perform. For instance, this could be `"action": "listNotifications"` or `"action": "getRandomRollRolls"`.
#### Any other parameters are optional and are specific to the module and action you are requesting
Many actions do not require additional parameters. For instance, `{"system": "notifications", "action": "listNotifications"}` will return a list of all of the current unread notifications (as JSON). However, there are some functions, such as `addNotification`, that require additional parameters (in this case `message`). To create a new notifications, one would use the following request:
```
{
  "system": "notifications",
  "action": "addNotification",
  "message": "Hello World!"
}
```

## Authentication
There are a couple ways to authenticate with the pineapple. Requests sent via the web interface use a PHPSESSID cookie as well as an X-XSRF-TOKEN header. The pineapple will verify that the session is valid and logged in and that the XSRF token matches the one generated at the start of the session. If both of these conditions are met, the request is routed. An example of a request sent by chrome is as follows:
```
POST /api/ HTTP/1.1
Host: 172.16.42.1:1471
Connection: keep-alive
Content-Length: 55
Accept: application/json, text/plain, */*
Origin: http://172.16.42.1:1471
X-XSRF-TOKEN: b01c5046faa2f8ffbed6f2fdd90a5605e6c505e3
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/49.0.2623.87 Safari/537.36
Content-Type: application/json;charset=UTF-8
Referer: http://172.16.42.1:1471/
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.8
Cookie: PHPSESSID=cfd6b0bb983666362cae311c457d1d34; XSRF-TOKEN=b01c5046faa2f8ffbed6f2fdd90a5605e6c505e3

{"system":"notifications","action":"listNotifications"}
```
This type of authentication is awkward and clumbsy to implement programmatically. Because of this, we have added a new way to authenticate with the WiFi Pineapple: API tokens. Though API tokens are supported by default, the pineapple is shipped without any valid tokens. The process of generating API tokens is simplified by the [API Tokens module](https://github.com/735tesla/Pineapple-API-Tokens-Module). After a token has been generated, it can be sent as an additional parameter. To use an API token, simply add an additional `apiToken` key to the request body. For example, to add a notification, one could send the following JSON request:
```
{
  "system": "notifications",
  "action": "addNotification",
  "message": "Hello World!",
  "apiToken": "7365626b696e6e652063616e7420636f6465202724ef6b5d7ac0b800cc83d474e8e007"
}
```
If the `apiToken` parameter is valid, the request will be route; otherwise an error will be returned.

## Modules
### Advanced
#### Description
Action|Description|Parameters
------|-----------|----------
`getResources`|Returns a JSON array of disk and memory usage|_none_
`dropCaches`|Clears system caches|_none_
`getUSB`|Returns a list of USB devices connected ot the pineapple|_none_
`getFstab`|Returns the contents of `/etc/config/fstab`|_none_
`getCSS`|Returns the contents of main.css|_none_
`saveFstab`|Overwrites `/etc/config/fstab` with a string|<ul><li>`fstab`<ul><li>A string to be written to `/etc/config/fstab`</li></ul></li></ul>
`saveCSS`|Overwrites the contents of main.css with a string|<ul><li>`css`<ul><li>A string to be written to `/pineapple/css/main.css`</li></ul></li></ul>
`checkForUpgrade`|Fetches the list of upgrades and the description of each|_none_
`downloadUpgrade`|Upgrades the pineapple to a specified firmare version (see output of `checkForUpgrades` and `getCurrentVersion`)|<ul><li>`version`<ul><li>The version to which the pineapple should be upgraded</li></ul></li></ul>
`getDownloadStatus`|Tells whether a firmware download is complete or in progress and how many bytes have been downloaded|_none_
`performUpgrade`|Upgrades using the image in /tmp/upgrade.bin|_none_
`getCurrentVersion`|Returns the current firmware version on the pineapple|_none_
### Clients
#### Description
### Configuration
#### Description
### Dashboard
#### Description
### Filters
#### Description
### Logging
#### Description
### ModuleManager
#### Description
### Networking
#### Description
### PineAP
#### Description
### Recon
#### Description
### Reporting
#### Description
### Tracking
#### Description

## Community Python API

## Further Information
