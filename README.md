# clevofan - Clevo Fan control module

Kernel module that provides fan control of various Clevo mainboards via standard hwmon interfaces (for using with generic fan control softwares like lm-sensors, pwmconfig, fancontrol, ...).

## Supported models
```bash
W35_37ET: supported and completely tested
W350SS:   not tested
P170SM:   not tested
```
* Teoretically supports all Clevo laptops but I have to add correct DMI_BOARD_NAME string and fan number to make module load without force_match parameter. Please open an issue "Add support for *model*" and provide test results, fan number and DMI_BOARD_NAME provided by dmidecode command and I'll add support (look "parameters" section for tests).

## Features

* Up to 3 fans supported

* FAN Speed Reading
  - Exposed hwmon device for reading fan speed provided by EC

* Fan Speed Control
  - Exposed hwmon PWM interface to make every fan control software capable to control the fan speed
  - pwmX-enable possible values are <br>
  1 -> manual speed <br>
  2 -> default EC automatic speed

## Parameters

* force_match [default:0] force driver to match with non-compatible mainboard, set number of fans to enable
  
## Please read CAREFULLY
This module executes write operations on the mainboard's Embedded Controller (EC). Thus reading is totally secure, issuing fan speed commands can teoretically put EC in a bad state until system is rebooted. This is caused by the nature of fan speed command, because is splitted in two different calls to EC: first specifies the fan, second one the speed. If another module/acpi stuffs issues a command between those two calls, EC response/action is unpredictable.

## Install
```bash
make
make install
```
## Load
```bash
modprobe clevofan
```
## Contributing
Advices and pull requests are welcome. You can contact me at pilia.simone96@gmail.com 
