# NB-IoT
## The module - SIM7070G NB-IoT
### Pinout
![alt text](https://www.waveshare.com/img/devkit/accBoard/SIM7070G-Cat-M-NB-IoT-GPRS-HAT/SIM7070G-Cat-M-NB-IoT-GPRS-HAT-details-13.jpg)

# Documentation
## User Manual
https://www.waveshare.com/wiki/SIM7070G_Cat-M/NB-IoT/GPRS_HAT

## Tutorial 
https://docs.iotcreators.com/docs/simcom-sim7070g-waveshare-dev-kit

## Sample Project
### Raspberry Pi Car with Python Tornado Websocket
https://github.com/wang1051992187/raspberry_pi_car


## MQTT Test (on public MQTT server)
```ruby
AT

OK
```
```ruby
AT+CPIN?

+CPIN: READY

OK
```
```ruby
AT+CGATT?

+CGATT: 1

OK
```
```ruby
AT+COPS?

+COPS: 0,0,"0041",9

OK
```
```ruby
AT+CGNAPN

+CGNAPN: 1,"m2mnb16.com.attz"

OK
```
```ruby
AT+CNCFG=0,1,”m2mnb16.com.attz”

OK
```
```ruby
AT+CNACT=0,1

OK

+APP PDP: 0,ACTIVE
```
```ruby
AT+CNACT?

+CNACT: 0,1,"10.94.36.44"
+CNACT: 1,0,"0.0.0.0"
+CNACT: 2,0,"0.0.0.0"
+CNACT: 3,0,"0.0.0.0"

OK
```