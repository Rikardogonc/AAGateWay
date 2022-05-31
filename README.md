# AAGateWay

Instructions : 

1. Close aastarter app no need anymore
2. Open AA developer settings and Start Headunit Server
3. Open aagateway on slave and change 1st option to "connecting mode"
4. Open wifi on slave and hotspot on master and once connection done plug your slave via usb cable to the car and the same wireless connection should happend

A modified version of [AAGateWay](https://github.com/borconi/AAGateWay) that requires [AAstarter](https://github.com/olivluca/AAstarter) on the master phone.

I only tested it on my car (with a MIB 2 headuint) and my phones. The master is a Xiaomi Redmi Note 4, the slave is a Motorola Moto E 2015 (surnia), both running
LineagesOs 17.1 (android 10).

The MIB 2 I have is quite peculiar: when it cannot establish a connection it will briefly remove power on the usb connector and that will upset
the apk released by Emil, hence the need to write this one.


The steps to make it work are:

1. open the app and ensure it is using the default options _LISTENING MODE_ and _USE IPV4_.
1. setup a hotspot on the slave.
1. configure the master to connect to said hotspot and to keep using it even if it has no Internet.
1. Install this app on the slave and AAstarter on the master.
1. Start AAStarter on the master and grant it the required permissions.
1. Connect the slave to the headunit.
1. When prompted confirm that you want to use AAGateway as the default application.
1. Wait for the master to be connected to the slave's hotspot.
1. Push the button to connect to the phone on the headunit.

It usually needs 2 o 3 (or more) tries before successfully establishing a connection.
None of the devices needs to be rooted.

The principle of operation is:

* when the headunit starts it, AAGateway will send a trigger on udp port 4455 to AAstarter on the master (actually it will send it to every connected station but
   1. only the master should be connected to this hotspot
   1. only the master will reply
* AAstarter will start Android Auto telling it to connect back to the slave.
* When the slave successfully initializes the connection with both partners (the headunit and the slave) it will start moving data between them.

If you set the _CONNECTING MODE_ option, then the app will work just like the original AAGateWay (it will connect to the headunit server that
you'll have to manually start on the master) but with the hotspot on the slave.

With the _USE IPV4_ option the app will only try ipv4 addresses to connect to the master, while with _USE IPV6_ it will only try ipv6 addresses.


=========================


below is the original README:

# AAGateWay

A super simple app which allows the connection to Android Auto over Wifi. It requires an Android Auto compatible car in the first place.

# License

You are free to use the code for personal use in any shape or form you want, and implement any modification you wish, however you are stictly forbiden in creating and publishing app with the same or similar purposer, regardless if the app is free or comrecial. If you wish to use the code in building and releaseing your own app, please seek written approval before proceeding.

# Copyright
Emil Borconi-Szedressy (C) 2017 - Wakefield - United Kingdom

# Requirements

* Android Studio 3.4.1 or higher
* Gradle 5.1.1
* Android API 27


# Build 

```
$> ./gradlew assemble 
```

This will generate an `apk` file inside build directory `./app/build/outputs/apk/debug`

# Install in debug device

```
$> ./gradlew installDebug
```
