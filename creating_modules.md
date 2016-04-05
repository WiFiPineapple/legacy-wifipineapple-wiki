# Creating WiFi Pineapple Modules

##Introduction
With the new WiFi Pineapple Interface, It is easy to create modules that use the new [API](api.md).
Modules use HTML, AngularJS and PHP to make requests and retrieve a response. The new interface and the modules also use Bootstrap.

// TODO: write better Introduction


##Anatomy of a basic module
A basic module will request information through AngularJS to PHP, and then the PHP will provide a response to AngularJS, where it will then be displayed on the HTML page for the user to see.

```
+-------------------+         +--------------+         +-----------+         +------+
| AngularJS Request |   -->   | PHP Response |   -->   | AngularJS |   -->   | HTML |
+-------------------+         +--------------+         +-----------+         +------+
```

A module will contain at least four files required to function. A `module.html` that contains the HTML for the module, A `module.info` that contains the name, description, version and author of the module in JSON format, a `module.js` file inside of the `js/` folder that contains the AngularJS, and finally a `module.php` file inside of the `php/` folder. It is structured like this:
```
.
├── js
│   └── module.js
├── module.html
├── module.info
└── php
    └── module.php
```
