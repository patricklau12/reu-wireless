# 1.　Install Jetson Nano
https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit

# 2. Test SIM7070 module with the Raspberry Pi
https://www.waveshare.com/wiki/SIM7070G_Cat-M/NB-IoT/GPRS_HAT#Use_it_with_Raspberry_Pi

## Testing with AT commands
Check the SIM7070_SIM7080_SIM7090_Series_AT_Command_Manual_V1.03.pdf for AT command list

# 3. (If it works with Raspberry Pi) Test with Jetson Nano
Check the pinout difference between Raspberry Pi 4 and Jetson Nano.
Use Jumper wires to connect the SIM7070 with Jetson Nano, if necessary.

And test the AT commands on Jetson Nano.

# 4. Register NB-IoT SIMs
If the AT command test is good, we can test the NB-IoT network
https://marketplace.att.com/app/register-sims

# Study
## What is MQTT
Two popular packages. You can also try to find out if there is a better way to do the MQTT, or other protocol 
### Mosquitto
### Paho MQTT


# (Extra / Prepare for 2nd week) Establish a communication link between Raspberry Pi/Jetson Nano devices over NB-IoT using MQTT.
Write a script to send data between two Jetson Nano, via NB-IoT network 

## Install MQTT
You would need to install MQTT on both Raspberry Pi devices. MQTT requires a broker (server) and one or more clients. You can use software like Mosquitto, a popular MQTT broker 

## The general architecture
The network structure may look like this. Or you can design a better one


[NB-IoT Device (SIM7070G + Jetson Nano + AT&T SIM)]{Client} ----> [AT&T NB-IoT Network (Access Network)] ----> [AT&T Core Network (EPC)] ----> [NB-IoT Device (SIM7070G + Jetson Nano + AT&T SIM)]{Server}


    +----------------+                             +----------------+
    |                |                             |                |
    | Raspberry Pi 1 |       NB-IoT Network        | Raspberry Pi 2 |
    | (MQTT Client)  |    <------------------>     | (MQTT Broker)  |
    | (Paho MQTT)    |                             | (Mosquitto)    |
    |                |                             |                |
    +----------------+                             +----------------+
         ^                                                  |
         |                                                  |
     Publishes                                          Subscribes to
      "topic/test"                                        "topic/test"




