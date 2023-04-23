# So what is this ? and why do I need it ?

Solis PV Inverters and AC Inverters have the option of installing a Solis data logger. These loggers come in a variety of versions with differing capabilities. All these data loggers allow you to use the Solis Cloud, ( https://www.soliscloud.com/ ). Typically the update frequency of the Solis Cloud and the data you send is every 15mins. Depending on your inverter you can ask for write access to the Solis cloud that allows you to change certain inverter parameters and settings. Unfortunately I have found Solis cloud to be somewhat buggy and in a constaint state of flux.

There are many ways to pull data from Solis Cloud into Home Assistant through using the Solis API, (detailed elsewhere) but there is no write option from Home Assistant to Solis cloud at this time. Why is this important, well if you have a Solis Battery Storage system you will find out pretty quickly that you are spending a lot of time manually configuring the charge times and options to optmises your Solar PV Generation and or your Off Peak Tariff Charging of your battery.

The solution detailed here is to allow your Home Assistant installation to control your Solis Battery Storage system, whilst at the same time retaining your Solis Cloud through your existing Solis Data Logger. If you dont want to retain your Solis Data Logger, or dont have one... then there are simpler ways to achieve this.

RS484 / Modbus consists of Slaves and Masters, the Solis Inverter is a Slave, and the Solis Data Stick is a Master, unfortunately the Home Assistant Connection is also a Master and on a RS485 bus, typically only one master is allowed. To therefore allow both the Solis Data Logger and the Homne Assistant connections to work, we need a way of allowing two masters on the RS485 bus.

# List of Parts Required

 1. Elfin-EW1X  (RS485/Modbus to WiFI Adapter
 2. GC-1201 RS485 / Modbus Dual Host Adapter
 3. Solis Data Logger
 4. Ginlong / Solis Plug and Socket
 5. Case
 6. 12v Regulated Power Supply
 7. Twisted Cable (CAT Cable will do)
 
 

#Block Diagram

![Block_Diagram](https://user-images.githubusercontent.com/118439620/233854313-77e940e0-4a45-4939-bf61-8ab2cae66072.jpg)


