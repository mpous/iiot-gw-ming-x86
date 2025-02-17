# MING (MQTT, InfluxDB, NodeRED and Grafana)

## Industrial IoT Gateway with Node-RED and MQTT broker running on balena

This is a project based on the [balena Node-RED block](https://github.com/balenablocks/balena-node-red) which supports the Node-RED [balena flow](https://github.com/balena-io-projects/node-red-contrib-balena) and works on x86 devices. 

### Disclaimer

This project is for *educational purposes only*. Do not deploy it into your premises without understanding what you are doing. USE THE SOFTWARE AT YOUR OWN RISK. THE AUTHORS AND ALL AFFILIATES ASSUME NO RESPONSIBILITY FOR YOUR SECURITY.

We strongly recommend you to have some coding and networking knowledge. Do not hesitate to read the source code and understand the mechanism of this project or contact the authors.

## Requirements

### Hardware

* Intel Nuc (`amd64`) and Generic x86 devices (still WIP for Raspberry Pi and similar)
* USB drive
* Power supply and (optionally) ethernet cable

### Software

* A balenaCloud account ([sign up here](https://dashboard.balena-cloud.com/))
* [balenaEtcher](https://balena.io/etcher)


## Deploy

You have two options here:

### One-click deploy via [Balena Deploy](https://www.balena.io/docs/learn/deploy/deploy-with-balena-button/)

You can deploy this project to a new balenaCloud application in one click using the button below:

[![](https://balena.io/deploy.svg)](https://dashboard.balena-cloud.com/deploy?repoUrl=https://github.com/mpous/iiot-gw-ming-x86)

Or, you can create an application in your balenaCloud dashboard and balena push this code to it the traditional way.

### In-control deploy via [balena CLI](https://www.balena.io/docs/reference/balena-cli/)

If you are a balena CLI expert, feel free to use balena CLI. This option lets you configure in detail some options, like adding new services to your deploy or configure de DNS Server to use.

- Sign up on [balena.io](https://dashboard.balena.io/signup)
- Create a new fleet on balenaCloud.
- Add a new device and download the image of the BalenaOS it creates.
- Burn the USB drive, connect it to the x86 device and boot it up (you might go to the BIOS to make the device to boot from the USB on the first time. Please read more here).

While the device boots (it will eventually show up in the Balena dashboard) we will prepare de services:

```
cd ~/workspace
git clone https://github.com/mpous/iiot-gw-ming-x86
cd iiot-gw-ming-x86
```

- Using [Balena CLI](https://www.balena.io/docs/reference/cli/), push the code with `balena push <fleet-name>`
- See the magic happening, your device is getting updated 🌟Over-The-Air🌟!


## Variables

### Device Variables

Variable Name | Default | Description
------------ | ------------- | -------------
PORT | `80` | the port that exposes the Node-RED UI
USERNAME | `balena` | the Node-RED admin username
PASSWORD | `balena` | the Node-RED admin password
ENCRIPTION_KEY | `balena` | the encription key used to store your credentials files

You **must** set the `USERNAME` and `PASSWORD` environment variables to be able to save or run programs in Node-RED.  

## Node-RED

For running Node-RED, use the local IP address on port 80, if you are on the same network than your device. You also can use the `Publick Device URL` by balena to access to the Node-RED UI.

Introduce the `USERNAME` and `PASSWORD` specified as a Variable on balenaCloud. The default are `balena`.

### Add Node-RED nodes needed

![Add Node-RED modbus nodes](https://user-images.githubusercontent.com/173156/164450054-4942088f-7965-4c6d-909f-cc2c3e0e59de.png)

If you need to add another library or nodes on your Node-RED. Open the top-right menu, click `Manage palette`. Go to the `Install` tab and search (e.g.) *node-red-contrib-modbus*. And click Install.

New blocks of nodes should appear on your left menu on new sections or not.

![New blocks on NodeRED](https://user-images.githubusercontent.com/173156/164450156-5d32115e-422f-4efb-9f3f-fcb8dbcd17ea.png)


### Use the MQTT broker

The MQTT broker is located on your localhost port 1883 or on the `mqtt` service running on the device.


### Start building your flows

Now you can start building your flows and deploy them to your gateway. You can find the flow, clicking `Import`, then `Local` and then `iiot-gw.json`. You also can find an example of the flows we built for a workshop [here](https://github.com/oriolrius/miot-nodered-demo).


## Attribution

- This is a result of a workshop made by [Oriol Rius](https://github.com/oriolrius) and [Marc Pous](https://github.com/mpous).
- This is based on the [balena Node-RED block](https://github.com/balenablocks/balena-node-red) made by Carlo Curinga and others. And also inspired by the [Razikus Node-RED](https://github.com/Razikus/balena-nodered) project.
- This is in joint effort between Carlo Curinga and Marc Pous to present in the [Node-RED Con 2021](https://nodered.jp/noderedcon2021/index-en.html).
