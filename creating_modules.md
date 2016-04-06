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

A module will contain at least four files required to function. A `module.html` that contains the HTML for the module, A `module.info` that contains the name, description, version and author of the module in JSON format, a `module.js` file inside of the `js/` folder that contains the AngularJS, and finally a `module.php` file inside of the `api/` folder. It is structured like this:
```
.
├── js
│   └── module.js
├── module.html
├── module.info
└── api
    └── module.php
```

Modules are stored on the WiFi Pineapple at `/pineapple/modules/`.

##Creating a module
You can create the module files on the WiFi Pineapple with ease using the [Module Maker](https://www.wifipineapple.com/modules) module. It will create the initial files for you (with an example included), and will also allow you to package the module for distribution when you are finished.

After downloading the module, enter the correct information into the Name, Description, Version and Author fields and click "Generate". Your module will then be ready to download and edit. Open the module in your favorite text editor.

#### module.html
The WiFi Pineapple modules make use of Bootstrap to provide a good mobile viewing experience and a clean look. Module developers are encouraged to make use of Bootstrap components, such as responsive tables and the grid system. To learn more about Bootstrap, visit the [Bootstrap Website](https://getbootstrap.com).

In this example we will make a `div` that is the width of the webpage. To do this, we will create a row, and then our `div` element which will use the `col-md-12` Bootstrap class.

Your code should look like this:
```
<div class="row">
    <div class="col-md-12">

    </div>
</div>
```

As the module is written with AngularJS, the HTML must be hooked up to a controller. For more information on AngularJS, visit the [AngularJS](https://angularjs.org) website.

To hook up the HTML to a controller, we will use our `div` element with the argument `ng-controller="ControllerName"`. For this example, our controller will be referred to as `ExampleController`. This div is now able to interact with your AngularJS inside of the `module.js` file.

Your code should now look like this:
```
<div class="row">
    <div ng-controller="ExampleController" class="col-md-12">

    </div>
</div>
```

Finally, we will use an expression called `hello`. This is done with `{{hello}}`. Later, we will use this expression to display text from our PHP. You can learn more at [AngularJS - Expression](https://docs.angularjs.org/guide/expression).

Our HTML code should now look like this:
```
<div class="row">
    <div ng-controller="ExampleController" class="col-md-12">
        {{ hello }}
    </div>
</div>
```

#### module.js
# TODO: Continue
