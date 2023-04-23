# So what is this ? and why do I need it ?

Solis PV Inverters and AC Inverters have the option of installing a Solis data logger. These loggers come in a variety of versions with differing capabilities. All these data loggers allow you to use the Solis Cloud, ( https://www.soliscloud.com/ ). Typically the update frequency of the Solis Cloud and the data you send is every 15mins. Depending on your inverter you can ask for write access to the Solis cloud that allows you to change certain inverter parameters and settings. Unfortunately I have found Solis cloud to be somewhat buggy and in a constaint state of flux.

There are many ways to pull data from Solis Cloud into Home Assistant through using the Solis API, (detailed elsewhere) but there is no write option from Home Assistant to Solis cloud at this time. Why is this important, well if you have a Solis Battery Storage system you will find out pretty quickly that you are spending a lot of time manually configuring the charge times and options to optmises your Solar PV Generation and or your Off Peak Tariff Charging of your battery.

The solution detailed here is to allow your Home Assistant installation to control your Solis Battery Storage system, whilst at the same time retaining your Solis Cloud through your existing Solis Data Logger. If you dont want to retain your Solis Data Logger, or dont have one... then there are simpler ways to achieve this without a lot of wiring.

RS485 / Modbus consists of Slaves and Masters, the Solis Inverter is a Slave, and the Solis Data Stick is a Master, unfortunately the Home Assistant Connection is also a Master and on a RS485 bus, typically only one master is allowed. To therefore allow both the Solis Data Logger and the Homne Assistant connections to work, we need a way of allowing two masters on the RS485 bus.

I assume you know your way around TCP/IP networks, can use a soldering iron, and have a multi-meter to check your wiring. NO LIABILITY WILL BE ACCECPTED IF YOU DAMAGE THE RS485 PORT ON YOUR INVERTER, DO THIS AT YOUR OWN RISK.

# List of Parts Required

 1. Elfin-EW1X  (RS485/Modbus to WiFI Adapter
 2. GC-1201 RS485 / Modbus Dual Host Adapter
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

# Elfin-EW1X

![En-küçük-elfin-ew10a-kablosuz-ağ-cihazları-modbus](https://user-images.githubusercontent.com/118439620/233855232-dc24a655-0af5-42e0-98a3-d3faa02b9795.jpg)

# Connecting it all up

![solis](https://user-images.githubusercontent.com/118439620/233855405-deb309dd-1b54-49ac-9ebf-71d98e47ed87.jpg)

There is no need for terminating resistors, (The RS485 splitter comes with some if you do).

# Elfin EL1* Config for Home Assistant

The Elfin adapater creates its own hotspot on startup, you will need to configure it for your own wifi network and use the settings below. PLEASE NOTE IT WILL NEED A STATIC IP. 

![Serial](https://user-images.githubusercontent.com/118439620/233855578-d6d0e1ac-9a60-4181-ab72-fd9846071a2f.png)
![Comms](https://user-images.githubusercontent.com/118439620/233855580-b00d36d7-f925-4189-90c5-e3d3ac699f94.png)

# Home Assistant

Whilst I wont go into installing Home Assistant and setup here ( there are many guides allready to do this)
I found the easiest way to intergrate with the Solis inverter is through installing SolaX, details can be found here: https://github.com/wills106/homeassistant-solax-modbus

Once Solax is installed, just configure it in the panel with the IP address of the ELFIN Wifi adapter (needs static IP) and the port number 502. Reload the plugin and you should see it connect all going well.

# What it all looks like..

![photo_2023-04-22_13-35-15](https://user-images.githubusercontent.com/118439620/233856214-688dc7b0-8fbf-49cd-b7b5-9f2588c692e4.jpg)

![342913273_464759539145371_8647742042126023905_n](https://user-images.githubusercontent.com/118439620/233856217-256645e0-d589-4145-813e-c3b004dbac04.jpg)

![342874861_572697404672110_3780646107351505346_n](https://user-images.githubusercontent.com/118439620/233856224-4145d521-abfa-4ecf-b20d-9500fd0f8a14.jpg)
