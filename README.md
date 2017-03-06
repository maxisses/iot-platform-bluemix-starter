Watson IoT Platform Starter for Bluemix with Node-RED Application
=================================================================

### Watson IoT Platform and Node-RED in Bluemix

Get started with [IBM Watson IoT platform](https://www.ibm.com/internet-of-things/platform/watson-iot-platform/) in Bluemix using this [Node-RED](http://nodered.org/) sample application that runs in a Node.js runtime. With the Starter, you can quickly simulate an Internet of Things device and generate sample data. Once you've deployed the [IBM Watson IoT Platform service](https://bluemix.net/catalog/services/internet-of-things-platform/), Node-RED and Cloudant data store using the instructions below, follow the Bluemix doc [Getting started with Watson IoT Platform Starter](https://www.ng.bluemix.net/docs/#starters/IoT/iot500.html#iot500) to learn how to register the sample device from withing Watson IoT Platform, modify the Node-RED flow, create cards, and begin analyzing and displaying data in the Watson IoT Platform dashboard.

Try it out for yourself right now:

### Deploy through Bluemix devOps

[![Deploy to Bluemix](https://bluemix.net/deploy/button_x2.png)](https://bluemix.net/deploy?repository=) (via JazzHub)

[![Create toolchain](https://bluemix.net/devops/graphics/create_toolchain_button.png)](https://bluemix.net/devops/setup/deploy?repository=) (via Continuous Delivery)

### Deploy from local command-line

Install all the required CLI tools: [Bluemix CLI](http://clis.ng.bluemix.net/), [cf CLI](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html), [git](https://git-scm.com/downloads), etc. 

More details in Bluemix docs [CLI and Dev Tools](https://bluemix.net/docs/cli/index.html).

Log into Bluemix:

```cf
cf api <your-base-bluemix-url>
cf login <your-bluemix-id@null>
```

Create the required services:

```
cf create-service iotf-service iotf-service-free iotp-starter`
cf create-service cloudantNoSQLDB Lite iotp-starter-cloudantNoSQLDB`
```

Clone this repository locally:

`git clone <this base URL>`

For example:

`git clone https://github.com/ibm-watson-iot/iot-platform-bluemix-starter`

Push the app to Bluemix:

`cf push <your app name>`

### How does this work?

When you click the button, you are taken to Bluemix where you get a pick a name
for your application at which point the platform takes over, grabs the code from
this repository and gets it deployed.

It will automatically create an instance of the IBM Watson Internet of Things (IoT) Platform service, call it
`iotp-starter` and bind it to you app. This is where all your IoT devices send their sensor data, and where Node-RED and other application get the IoT data sent from. If you deploy multiple instances of
Node-RED from this repository, they will share the one Watson IoT Platform instance.

It will automatically create an instance of the Cloudant service, call it
`iotp-starter-cloudantNoSQLDB` and bind it to you app. This is where your
Node-RED instance will store its data. If you deploy multiple instances of
Node-RED from this repository, they will share the one Cloudant instance.

It includes a set of default flows that are automatically deployed the first time
Node-RED runs.


### Customising Node-RED

This repository is here to be cloned, modified and re-used to allow anyone create
their own Node-RED based application that can be quickly deployed to Bluemix.

The default flows are stored in the `defaults` directory in the file called `flow.json`.
When the application is first started, this flow is copied to the attached Cloudant
instance. When a change is deployed from the editor, the version in cloudant will
be updated - not this file.

The web content you get when you go to the application's URL is stored under the
`public` directory.

Additional nodes can be added to the `package.json` file and all other Node-RED
configuration settings can be set in `bluemix-settings.js`.

If you do clone this repository, make sure you update this `README.md` file to point
the `Deploy to Bluemix` button at your repository.

If you want to change the name of the Cloudant instance that gets created, the memory
allocated to the application or other deploy-time options, have a look in `manifest.yml`.
