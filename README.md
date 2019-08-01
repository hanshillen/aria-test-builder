# HTML5 ARIA Test Builder
This Node.js application generates test cases for accepted [ARIA][aria] (Accessible Rich Internet Application) role and aria=* attributes on elements defined in HTML5.

The test cases for each HTML element are sent to the [NU Validator][nuvalidator]. The application flags test cases where the NU Validator's results are inconsistent with current ARIA conformance requirements. 

## Installation
To run the application on local machine, system requires Java8 installed.

```sh
~$ java -version
java version "1.8.0_221"
Java(TM) SE Runtime Environment (build 1.8.0_221-b11)
Java HotSpot(TM) 64-Bit Server VM (build 25.221-b11, mixed mode)
```

If Java version differs, download and set Java 8 as the default version used on your system.

To change Java 8 version on Windows: 

* Start -> Control Panel -> System -> Advanced

* Click on Environment Variables, under System Variables, select PATH, and click Edit button.

* In Edit Environmental Variable window, modify PATH by adding the location of your Java /bin directory. The location of JRE directory will be something similar to `C:\Program Files\Java\jre1.8.0_221\bin`

* Open new command shell and check Java version.

After Java 8 is installed, the Node.js application can run. In command shell, navigate to the root level of the project directory.

```sh
// install node modules
~$ npm install

// run the application
~$ grunt
Running "prompt:init" (prompt) task
? choose a task (Use arrow keys)
> Create Individual Test Cases
  Validate Individual Test Cases
  Generate Mistakes Report for Individual Test Cases
  All of the Above (Individual)
  ──────────────
  Create Mega Test Case
  Validate Mega Test Case
  Generate Mistakes Report for Mega Test Case
  All of the Above (Mega)
```

## How It Works

Grunt is a runtime environment for automating tasks. The first Grunt task is to create a page for each HTML element with individual test cases for every ARIA=* and role attribute. These unique pages are built out of Handlebars templates in `/src/templates`.

The next Grunt task takes each HTML page and sends this HTML,more precisely, its serialized DOM, to the Nu Validator. The Nu Validator tests each page for accepted ARIA attributes.

The final Grunt task is flagging test cases where the Nu Validator incorrectly assessed an ARIA attribute. The Nu Validator should match the rules set in the `/src/elements-roles.json` and `/src/roles-states.json`.

The JSON files must be periodically updated to reflect updates to ARIA.

[aria]: https://www.w3.org/TR/html-aria/
[nuvalidator]: https://validator.w3.org/nu/