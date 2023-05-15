# So what is this ? and why do I need it ?

Solis PV Inverters and AC Inverters have the option of installing a Solis data logger. These loggers come in a variety of versions with differing capabilities. All these data loggers allow you to use the Solis Cloud, ( https://www.soliscloud.com/ ) and also view your stats in a mobile app. Typically the update frequency of the Solis Cloud and the data you send is every 15mins. Depending on your inverter you can ask for write access to the Solis cloud that allows you to change certain inverter parameters and settings. Unfortunately I have found Solis cloud to be somewhat buggy and in a constaint state of flux, and would like my statistics in as near real time as possible, I would also like to make smart decisions on when my battery storage system charges from the grid.

There are many ways to pull data from Solis Cloud into Home Assistant through using the Solis API, (detailed elsewhere) but there is no write option from Home Assistant to Solis cloud at this time. Why is this important ?, well if you have a Solis Battery Storage system you will find out pretty quickly that you are spending a lot of time manually configuring the charge times, and options to optmise your Solar PV Generation and / or your Off Peak Tariff Charging of your battery storage.

The solution detailed here is to allow your Home Assistant installation to control your Solis Battery Storage system and log data statistics locally in near real time, whilst at the same time retaining your Solis Cloud through your existing Solis Data Logger. If you dont want to retain your Solis Data Logger, or dont have one... then there are simpler ways to achieve this without a lot of wiring. (not detailed here).

The RS485 / Modbus comms consist of Slaves and Masters, the Solis Inverter is a Slave, and the Solis Data Stick is a Master, unfortunately the Home Assistant Connection is also a Master and on a RS485 bus, typically only one master is allowed. To therefore allow both the Solis Data Logger and the Home Assistant connections to work without issues or loosing data, we need a way of allowing two masters on the RS485 bus.

I will assume you know your way around TCP/IP networks, have Home Assistant allready installed, can use a soldering iron, and have a multi-meter to check your wiring. NO LIABILITY WILL BE ACCECPTED IF YOU DAMAGE THE RS485 PORT ON YOUR INVERTER, DO THIS AT YOUR OWN RISK.

# List of Parts Required

 1. Elfin-EW11  Make sure its the RS485 versions. (RS485/Modbus to WiFI Adapter)
 2. GC-1201 RS485 / Modbus Dual Host Adapter (make sure its the two masters one slave version).
 3. Solis Data Logger
 4. Ginlong / Solis Plug and Socket
 5. Case
 6. 12v Regulated Power Supply
 7. Twisted Cable (CAT Cable will do)
 
 Most of these parts you can get from Alliexpress or Ebay..

# Block Diagram

![Block_Diagram](https://user-images.githubusercontent.com/118439620/233854313-77e940e0-4a45-4939-bf61-8ab2cae66072.jpg)

# Solis  / Ginlong Plug and Socket

![exeedconn](https://user-images.githubusercontent.com/118439620/233855102-5a18d3e9-6aa1-44e2-9918-01a01b63efcb.png)

# GC-1201K RS485 / Modbus Dual Host Adapter

![30184964](https://user-images.githubusercontent.com/118439620/233855180-48cb40f2-3c9e-4b50-9c8e-d85f422f4d14.jpg)

There are three models of these devices available, make sure you buy the correct version, (GC-1201) so this is the link to the one I bought: https://www.aliexpress.com/item/1005005128549371.html?spm=a2g0o.productlist.main.1.353847f3QnMMn4&algo_pvid=60b48212-7e50-4f36-a683-2d5b3f50ac56&algo_exp_id=60b48212-7e50-4f36-a683-2d5b3f50ac56-0&pdp_npi=3%40dis%21GBP%2122.75%2120.93%21%21%21%21%21%40211bd8be16824105524221086d07da%2112000031771589334%21sea%21UK%21164589609&curPageLogUid=ZJza73apo6la

There is a windows app to configure the hub, but it is in Chineese, but there is no need to tinker with it as the defaults work fine for this application.

Chinese Manual: https://greatcontroltech.com/filedownload/644365
Configuration Tool, (Chinese) https://greatcontroltech.com/filedownload/644366  (not required for the application)

# Elfin-EW11

![images (1) jpers485](https://user-images.githubusercontent.com/118439620/233860581-a5dc78f6-2aaa-4502-b845-95e5ef474e98.jpeg)


# Connecting it all up

![solis](https://user-images.githubusercontent.com/118439620/233855405-deb309dd-1b54-49ac-9ebf-71d98e47ed87.jpg)

There is no need for terminating resistors, (The RS485 splitter comes with some if you do).

# Solis RS485 / Modbus Connector

This port is a green port located externally on all Solis inverters on the bottom of the inverter.  
Pin 1 = +5 volts DC
pin 2 = -5 volts DC 
Pin 3= +RS485
Pin 4 = -RS485
Checking the voltage on pins 1 and 2 with a multimeter will ensure power is provided to the communication device (ex: wifi datalogger. The voltage reading should be 5V on DC.
 
Checking the voltage on pins 3 and 4 with a multimeter will ensure RS485 signal between the inverter and the communication device. RS-485 voltage should read ~1.7Volts on DC  
 

![plug](https://user-images.githubusercontent.com/118439620/234095297-eb31c271-2cd4-4ae7-a01a-4713d24f9b78.png)


![Qnj0q0FOZYWB603nZCFglUWanluht1yDXQ](https://user-images.githubusercontent.com/118439620/233996798-17b65f67-b93c-47ab-b19d-1abcf0fe85e6.png)



# Elfin EW11 Config for Home Assistant

The Elfin adapater creates its own hotspot on startup, you will need to configure it for your own wifi network and use the settings below. PLEASE NOTE IT WILL NEED A STATIC IP. 

![Serial](https://user-images.githubusercontent.com/118439620/233855578-d6d0e1ac-9a60-4181-ab72-fd9846071a2f.png)
![Comms](https://user-images.githubusercontent.com/118439620/233855580-b00d36d7-f925-4189-90c5-e3d3ac699f94.png)

# Home Assistant

Whilst I wont go into installing Home Assistant and setup here ( there are many guides allready to do this)
I found the easiest way to intergrate with the Solis inverter is through installing SolaX, details can be found here: https://github.com/wills106/homeassistant-solax-modbus

Once Solax is installed, just configure it in the panel with the IP address of the ELFIN Wifi adapter (needs static IP) and the port number 502. Reload the plugin and you should see it connect all going well.

To pull weather into Home Assistant I use Solcast..   you can then use the forecast and create an automation to set the charging of your Solis Battery Storage.

# What it all looks like..

![photo_2023-04-22_13-35-15](https://user-images.githubusercontent.com/118439620/233856214-688dc7b0-8fbf-49cd-b7b5-9f2588c692e4.jpg)

![342913273_464759539145371_8647742042126023905_n](https://user-images.githubusercontent.com/118439620/233856217-256645e0-d589-4145-813e-c3b004dbac04.jpg)

![342874861_572697404672110_3780646107351505346_n](https://user-images.githubusercontent.com/118439620/233856224-4145d521-abfa-4ecf-b20d-9500fd0f8a14.jpg)
