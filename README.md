# Hybreed
Hybreed is a framework to develop swift and good looking hybrid mobile apps. It's Cordova based and use the latest front-end techologies: Gulp, ES6, Browserify, BrowserSync, SASS...

To achieve the best performance it uses Backbone as the main JavaScript library to build the application's logic.

## Prior knowledge

For a better understanding of the framework, it's necessary to know the basics of:
* HTML5 y CSS
* Javascript
* Backbone
* Apache Cordova

## Installation

In order to start to use the framework, clone the repository and install all the dependencies. All of them can be founded in the package.json file, so to install all of it, it's only necessary to run:

```
npm install
```

## Hybreed Application Structure

Hybreed it's a framework built on the base of several technologies. Using this set of technologies, it's posible to build hybrid mobile applications, with a great performance, and as native looking as desired.

### Directory Tree

```
Hybreed
 ├── gulp
 │   ├── tasks
 │   └── index.js
 ├── hooks
 │   └── ...
 ├── node_modules
 │   └── hybreed-core-modules
 ├── platforms
 │   └── ...
 ├── plugins
 │   └── ...
 ├── src
 │   ├── common
 │   │   └── ...
 │   ├── fonts
 │   │   └── ...
 │   ├── modules
 │   │   └── ...
 │   ├── vendor
 │   │   └── ...
 │   ├── index.html
 │   ├── main.js
 │   └── main.scss
 ├── test
 │   └── ...
 ├── www
 │   └── ...
 ├── .eslintrc
 ├── config.xml
 ├── package.json
 └── ...
```

The project it's based on nodeJS and Apache Cordova, so it keeps an structure that it's defined by those systems. The main folders and files on the project are:

* gulp: Gulp it's used to perform different tasks that improve the functionality of the framework.
* hooks: Scripts that allows to make modifications on the project on the diferent phases of the lifeclycle of the app.
* node_modules: All the modules referenced on the package.json file are installed in this folder.
* platforms: Folder that contains the native projects of the app.
* plguins: Add-on code that provides JavaScript interface to native components. It's auto generated by gulp from src folder.
* src: The application developed source code.
* www: The source code that will be executed as the hybrid application.
* .eslintrc: File that defines the rules that will be executed as an static code analysis.
* config.xml: It contains the application information.
* package.json: It holds all the project information, including all the project local dependencies.

### Gulp

On the following section, we'll detail the public tasks defined on gulp.

#### Develop

This task assists on the application's development:

```
gulp develop
```

It's configured as the default task on the project, so it's possible to statt it just with the command:

```
gulp
```

It performs the following actions:

* Set the debug mode.
* Cleans the *www* folder.
* Launch the esLint review, to check that the source code fulfill the defined rules.
* Compile de SCSS styles to CSS.
* Copy the index.html file (entry point for the application) and the text fonts.
* Generates the Javascript code.
* Copy all the outputs to the *www* folder.
* Opens the default navigator with a preview of the app.
* Watches any change on the source code in order to reload the navigator and show any performed change.


#### Production

This task generates a source suitable to be used on a porduction enviroment.

```
gulp production
```

Performs quite similar actions to the develop tasks, but it also includes the optimization, and obfuscation of the code.

* Cleans the *www* folder.
* Launch the esLint review, to check that the source code fulfill the defined rules.
* Compile de SCSS styles to CSS.
* Copy the index.html file (entry point for the application) and the text fonts.
* Generates the Javascript code.
* Optimizes and obfuscates the source code.
* Copy all the outputs to the *www* folder.


#### Test

With this task the unit tests written for the application will be executed.

```
gulp test
```

It performs the following actions:

* Starts the Karma sever.
* Prepares the PhantomJS browser.
* Execute the unit tests.
* Shows the full test report.

### Source Code

#### Dependency Management

To manage or install new packages on the project it's used the node package manager *npm*. Also, the projects uses *browserify*, so any third party library desired to install on the project, it's possible to do through npm also.

To add new libraries or packages on the project, it's only necessary to use the npm command to install and save a new package:

```
npm install <package> --save
```
This command will install the node package on the project, and also will add it to the package.json file, with all the others dependencies.

To use this new package through the application, at the start of the module in which you want to use it, write:

```
import <package> from '<package>'
```

#### Common

On this folder are stored the common styles of the application and the initialization file for the app.

#### Vendor

It contains the initialization of the packages and libraries used on the framework. On *libs.js* are included all the main ones of the framework, and exported to be used on every other module that could be on need of them.

To include a new package, it will be necessary to import it as explained on [Dependency Management](#dependency_management) section.

If the package it's a custom one, it could be included in a folder on this path, and referenced with a relative path:

```
import <package> from '~/src/vendor/<package>/<package file>'
```

After that no matter if it's a custom package or a third party one, include it on the export section, to be able to use it on any other module.

```
export {
    _,
    Backbone,
    Marionette,
    Broker,
    Hybreed,
    Snap,
    ionRangeslider,
    <New Package>
};
```

#### MhyC Library

The framework uses the MhyC (Mobile Hybreed Core) library tools exported as Hybreed.

This library includes some useful functions to develop a mobile application. This functions are:

* init: Initialize the library parameters.
* start: Sets the environment to perform different actions over native device.
* checkNet: Checks if the device has network connection
* getLocation: Gets the device's location.
* getPlatform: Gets the device platform (Android, iOS, Windows...)
* millisecondsToTime: Converts a date on milliseconds to a "normal" date.
* detectDevice: Returns if the device it's a phone or a tablet.
* isLandscapedTablet: Detects if the device it's a landscape tablet.
* getPressEvent: Gets the type of press event, depending on de OS.
* isIOS: Checks if the device is iOS.
* isAndroid: Checks if the device is Android.
* UI
    * generateScroll: Sets a view scroll, using iScroll library if necessary.
    * createSpinner: Creates a spinner to be used through the application on loading times.
    * showSpinner: Shows the created spinner.
    * hideSpinner: Hides the created spinner.
    * addClearButton: Creates a X to show on forms, and clear it.
    * toggleInput: Adds or removes a CSS class.
* Analytics
    * setTrackingID: Sets the Google Analytics tracking ID.
    * trackView: Tracks a view.
    * trackEvent: Tracks an event.
    * addCustomDimension: Adds a custom metric.
* Push
    * setOnNotification: Receives a function that sets the behaviour when a push notification arrives.
    * setConfig: Sets the configuration parameters for push notifications.
    * init: Initialize the application push notifications settings, with the parameters set on the configuration method.

#### Fonts

This folder holds the different fonts used on the application.

#### Modules

A module it's a new view or big functionality of the app. In all cases it's formed by a *index.js* main controller, and a *views* folder that includes its associated files.

This views, in general, are formed by one or more than one html, a scss and a javascript file.
* The HTML file it's the skeleton of the view, and uses _ to the pattern design.
* The SCSS file contains the styles of the view. When it's processed a CSS file will replace the SCSS. It also possible to create the view styles on CSS instead of SCSS.
* The javascript files contains the view's logic.

#### Broker

The communication between views it's made through the Backbone Broker. It uses an event system to communicate different contexts or views.

To use this Broker, it's necessary to import it on every module controller header, as Backbone itself, along all other libraries suitable for use on that module.

```
import {Backbone, Broker} from '~/src/vendor/libs';
```

After that, to declare functions using the Backbone, it's necessary to do through a channel with the name of the module, so can be accessed from other modules or contexts.

```
Broker.channel('<module>')
```

Those functions that can be used with Broker are:

* on: With this method the channel register which functions will be called on a trigger event.
```
Broker.channel('<module>').on({
    <function to execute on trigger event>,
    <function to execute on trigger event>,
    ...
});
```
* trigger: Triggers the execution of a function declared on a channel thorough an *on*. The function declared in *on* method to execute it's the one with the same name invoked on the *trigger* method.
```
Broker.channel('<module>').trigger('<function name>');
```
* reply: The channel registers function to get information regarding it's view.
```
Broker.channel('<module>').reply({
    <function to execute on request event>,
    <function to execute on request event>,
    ...
});
```
* request: Triggers the execution of a function declared on a channel thorough an *replay*, to get some information. The function to execute it's the one with the same name invoked on the *reply* method.
```
Broker.channel('<module>').request('<function name>');
```

#### Screen

This is the basic module of the application. In some form, other modules inherit it.

It includes the application header, with the controllers for the left and right header buttons, and the option to show or not the menu. On the module initialize function, all this options can be set or hide at desire on every view.

To do so, if a view have to inherit from screen, on the view's show method it's necessary to summon the start method of the screen's Broker channel, with the desired parameters (header tittle, button right, button left, menu...).

```
Broker.channel('screen').trigger('start', {
        type: '<normal or without header>',
        title: '<View title>',
        leftButtonOpts: {
            class: 'fa fa-chevron-left',
            callback() {
                <Function to invoke on the button press>
            },
            ...
        },
        rightButtonOpts: {
            class: 'fa fa-chevron-left',
            callback() {
                <Function to invoke on the button press>
            },
            ...
        },
        contentView: <Declared view>,
        ...
});
```

It's possible to add new options to the screen view if it would be necessary.

#### Main

The *main.js* file contains the imports of all vendor libraries, all modules, and the app configuration file. Also, when the DOM it's ready, starts Hybreed library to perform all configuration settings of the mobile app, and the begin of it's execution.

#### esLint

esLint file include the rules configuration for the Static Code Analysis.

More information about esLint rules and it's configuration can be found [here](http://eslint.org/docs/rules/ "esLint").

#### Tests

The unit tests of the mobile app can be found on the *test* folder. The *tests.js* file, setups the environment and global viaribales needed for all the tests. Also, on *utils* folder it's held a configuration file to perform actions and initialize the dom through *jsdom* library.

Every module suitable to have unit tests, should a file with the name *< module >.spec.js*. The tests are developed with *sinon* and *chai*. On the header it's necessary to import the module object of the tests, and it's view if it had any and have tests to be executed on it:

```
import <Module> from '~/src/modules/<module>/index';
import <ModuleView> from '~/src/modules/<module>/views/<module>'
```

After that, all variables and configurations needed for the tests should be initialized with the necessary data or configuration. Every test should have the following schema:

```
it('<Short tests description>', () => {
        // Having
        <Starting conditions>
        // Then
        <If necessary, actions performed to achieve the final result>
        // Expect
        <Expected result or execution>
});
```


## Apache Cordova Commands

We'll make a brief summary of the main Apache Cordova commands to simplify the task of building applications with the framework.

In order to launch the application on any mobile device, first it's necessary to create the native platforms for each OS we desire, with the following command:

```
cordova platform add <android|ios|windows>
```

To run the application on a device, on iOS or Windows it's better to do through it's IDEs (XCode and Visual Studio). On Android, it's possible to use de following command:

```
cordova platform run <android>
```

If during the development of the application, there are changes that we need to test on the device, and the platform it's already added, to include the new code it's necessary to use:

```
cordova platform prepare <android|ios|windows>
```

Also, in case that during the development appears the need to install a Cordova plugin, it's possible to do through the following command:
```
cordova plugin add <cordova-plugin-name> --save
```



