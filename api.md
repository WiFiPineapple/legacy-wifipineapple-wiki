# WiFi Pineapple Module API
#TODO: Add available destinations for ModuleManager.

## Introduction
Unlike the old web interface, the back end of the new interface has been decoupled from the front end. All requests to perform system actions are sent as POSTs to `/api/`. The content of the POST is JSON and contains a minimum of two parameters.
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
_(Please note that extra authentication parameters are not required when using the angular module api due to the fact that client side module components are loaded after the user authenticates their browser)_

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
The advanced module simplifies some more advanced processes like performing system upgrades and clearing system caches. FOr example, the following will clear the pineapple's caches:
```
{
  "module": "Advanced",
  "action": "dropCaches"
}
```
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
The Logging module provides easy access to the syslog, dmesg, PineAP and Reporting logs. To use these API functions, send your api request with the "module" set to "Logging":
```
{
    "module": "Logging",
    "action": "getSyslog",
}
```
Action|Description|Parameters
------|-----------|----------
`getSyslog`|Return the system log in full|_none_
`getDmesg`|Return the kernel log in full|_none_
`getReportingLog`|Return the log from the Reporting module|_none_
`getPineapLog`|Return the log from PineAP|_none_
`clearPineapLog`|Clear the PineAP log file|_none_
`getPineapLogLocation`|Return the location of the PineAP log|_none_
`setPineapLogLocation`|Set the location for PineAP logging|<ul><li>`location`<ul><li>New location of PineAP log.</ul></li></ul></li>
### ModuleManager
#### Description
The Module Manager is responsible for installing, removing, and upgrading modules. It's API can be used to manage modules, as well as fetching the list of installed modules and getting available modules. To use them in your module, your request body would look like this:
```
{
    "module": "ModuleManager",
    "action": "removeModule",
    "moduleName": "Module"
}
```

Action|Description|Parameters
------|-----------|----------
`getAvailableModules`|Return an array of modules available for download|_none_
`getInstalledModules`|Return an array of modules currently installed|_none_
`downloadModule`|Download a specified module|<ul><li>`moduleName`<ul><li>Name of module to install</li></ul></li></ul><ul><li>`destination`<ul><li>Destination of module.</li></ul>
`installModule`|Install a specified module|<ul><li>`moduleName`<ul><li>Name of module to install</li></ul></li></ul><ul><li>`destination`<ul><li>Destination of module.</li></ul>
`removeModule`|Remove a specified module|<ul><li>`moduleName`<ul><li>Name of module to remove</ul></li></ul></li>
`downloadStatus`|Check status of module download|_none_
`installStatus`|Check status of module install|_none_
`checkDestination`|Check if the specified destination has the specified space free|<ul><li>`name`<ul><li>Name of module</ul></li></ul></li><ul><li>`size`<ul><li>Size of module</ul></li></ul></li>
### Networking
#### Description
The Networking module API allows you to interface with the networking side of the WiFi Pineapple without having to write your own functions to manage interfaces, the DNS, and the routing table. As described above, you can use these actions in your own module like so:
```
{
    "module": "Networking",
    "action": "setHostname",
    "hostname": "Pineapple"
}
```

Action|Description|Parameters
------|-----------|----------
`getRoutingTable`|Returns the routing table of the Pineapple|_none_
`restartDNS`|Restarts the DNS service on the Pineapple|_none_
`updateRoute`|Updates the routing table|<ul><li>`routeIP`<ul><li>IP Address for the route</li></ul></li></ul><ul><li>`routeInterface`<ul><li>Interface for the route</ul></li>
`getAdvancedData`|Returns the hostname and ifconfig|_none_
`setHostname`|Sets the hostname for the Pineapple|<ul><li>`hostname`<ul><li>String for the hostname</li></ul></li></ul>
`resetWirelessConfig`|Resets the Wireless Configuration for the Pineapple|_none_
`getInterfaceList`|Returns an array of available network interfaces|_none_
`saveAPConfig`|Writes properties to the AP configuration|<ul><li>`selectedChannel`<ul><li>Channel for the AP to operate on</li></ul></li></ul><ul><li>`openSSID`<ul><li>String for the SSID of the Open Access Point</li></ul></li></ul><ul><li>`hideOpenAP`<ul><li>Boolean to hide the Open Access Point or not</li></ul></li></ul><ul><li>`managementSSID`<ul><li>String for the SSID of the Management AP</li></ul></li></ul><ul><li>`managementKey`<ul><li>string for the WPA2 passphrase for the Management AP</li></ul></li></ul><ul><li>`disableManagementAP`<ul><li>Boolean to disable the Management AP or not</li></ul></li></ul>
`getAPConfig`|Returns an array of properties from the access point configuration.|_none_
`getMacData`|Returns the MAC Addresses of each of the wireless interfaces|_none_
`setMac`|Sets the MAC address for a specified interface|<ul><li>`random`<ul><li>Boolean to set the MAC address as a random value.</li></ul></li></ul><ul><li>`interface`<ul><li>The interface you want to change the MAC address of</li></ul></li></ul><ul><li>`mac`<ul><li>The new MAC address of the interface</li></ul></li></ul>
`resetMac`|Reset the specified interface's MAC address to the factory default.|<ul><li>`interface`<ul><li>The interface to reset</li></ul></li></ul>

### PineAP
#### Description
The PineAP module provides an easy way to interface with the [PineAP suite](/#!index.md#The_PineAP_Suite). For example, one might use the following to add an SSID to PineAP's pool:
```
{
  "module": "PineAP",
  "action": "addSSID",
  "ssid": "ACME WiFi"
}
```
Action|Description|Parameters
------|-----------|----------
`getPool`|Returns an array of the SSIDs in PineAP's pool|_none_
`clearPool`|Clears the PineAP pool|_none_
`addSSID`|Adds an SSID to the pool|<ul><li>`ssid`<ul><li>The SSID string to add</li></ul></li>
`removeSSID`|Removes an SSID from the pool|<ul><li>`ssid`<ul><li>The SSID string to remove</li></ul></li>
`setPineAPSettings`|Update PineAP's settings|<ul> <li>`settings` <ul> <li>A dictionary with setting key/value pairs <ul> <li>`allowAssociations` <ul> <li>Whether clients should be allowed to associate to the pineapple</li> </ul> </li> <li>`logProbes` <ul> <li>Whether to log probe requests</li> </ul> </li> <li>`logAssociations` <ul> <li>Whether to log associations</li> </ul> </li> <li>`beaconResponses` <ul> <li>Whether to send beacon responses</li> </ul> </li> <li>`captureSSIDs` <ul> <li>Whether to add sniffed SSIDs to the pool</li> </ul> </li> <li>`broadcastSSIDs` <ul> <li>Whether to broadcast the SSID pool</li> </ul> </li> <li>`beaconInterval` <ul> <li>The beacon interval- must be one of "low", "normal" or "aggressive"</li> </ul> </li> <li>`responseInterval` <ul> <li>The response interval- must be one of "low", "normal" or "aggressive"</li> </ul> </li> <li>`targetMAC` <ul> <li>The MAC to target with responses</li> </ul> </li> <li>`sourceMAC` <ul> <li>The MAC PineAP should spoof</li> </ul> </li> </ul> </li> </ul> </li></ul>
`getPineAPSettings`|Returns a dictionary with all the current PineAP settings|_none_
`deauth`|Deauth a list of clients from a station. **_Use this with caution. The misuse of this function may be illegal in some places._**|<ul><li>`sta`<ul><li>The bssid of the station from which to disconnect the clients</li></ul></li><li>`clients`<ul><li>An array of client MACs to deauth</li></ul></li><li>`multiplier`<ul><li>The number of deauths (from 1 to 10) to send</li></ul></li><li>`channel`<ul><li>The channel to hop to before sending the frame(s)</li></ul></ul></li></ul>
`enable`|Enables PineAP|_none_
`disable`|Disables PineAP|_none_
`saveAsDefault`|Makes the current configuration persist after reboots|_none_
`downloadPineAPPool`|Get a download link to the SSID pool (useful for client side modules)|_none_
### Recon
#### Description
### Reporting
#### Description
### Tracking
#### Description

## Community Python API

## Further Information
