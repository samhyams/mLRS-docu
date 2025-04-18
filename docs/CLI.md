# mLRS Documentation: CLI Commands #

([back to main page](../README.md))

Besides the mLRS Lua script, which however is not available for all radio transmitters, the CLI is the main method for configuring the mLRS Tx modules and receivers.

The CLI commands consist of one or more strings, each separated by a blank, and a terminating character. The terminating character can be '\r' (carriage return), '\n' (line feed), ',' or ';'. The CR/LF line feed handling depends very much on the terminal which is being used and its configuration. Hence, it is good practice to just always terminate the CLI commands with, e.g., a ';' (this will be done for the commands listed below). The CLI is case sensitive, except for parameter names. That is, the commands need to be entered lower case, but parameter names can be entered with any letter case.

The serial settings are: baudrate 115200 bps, 8 data bits, no parity, 1 stop bit (8N1).

The CLI uses CRLF for terminating lines. 

Depending on the device, some parameters are not available for configuration or cannot be changed. For instance, for a device which does not support a buzzer the parameter "Buzzer" is not available, and for a device which does not support diversity the parameter "Diversity" cannot be changed. Parameters which are not available are displayed with a value "-", and parameters which cannot be changed are displayed with the current selection but a comment "(unchangeable)" in addition.

> [!IMPORTANT]
> Parameter changes become permanent by invoking pstore; (else they are lost with the next power cycle). 

Many parameters require a power cycle to become effective. Ergo, one essentially should finish a parameter change session with pstore; if one is happy with the made changes.

## Commands ##

#### h; or help; or ?; #### 
Lists the available commands, with a very brief description

#### v; #### 
Prints the device name and firmware version for the Tx module and, if connected, also the receiver.

#### pl; #### 
Lists all parameters and their settings. Comment: The parameters of the receiver are listed only if a receiver is connected, else a warning message is printed.

#### pl c; #### 
Lists the shared parameters, i.e., those parameters which are common for both the Tx module and the receiver, and their settings. Comment: If a receiver is not connected, a warning message is printed.

#### pl tx; #### 
Lists the parameters of the Tx module and their settings. 

#### pl rx; #### 
Lists the parameters of the receiver and their settings. Comment: These parameters are listed only if a receiver is connected, else a warning message is printed.

#### p name; or p name = ?; #### 
Prints the setting of the parameter with name 'name'. Comment: Blanks in the parameter name should be replaced by '_'. E.g., the setting for the parameter "Tx Power" would be obtained with the CLI command p tx_power;.

#### p name = value; #### 
Changes the setting of the parameter with name 'name' to the specified value. Comment: Blanks in the parameter name should be replaced by '_'. E.g., the setting for the parameter "Tx Power" would be changed to zero with the CLI command p tx_power = 0;.

#### pstore; #### 
Stores the new parameter settings into the Tx module and, if connected, also into the receiver.

#### setconfigid; #### 
Set the Configuration ID of the Tx module.

#### bind; #### 
Starts the binding. Comment: Only the Tx module is set into binding mode. The receiver must be put into binding mode by pressing its bind button.

#### reload; #### 
Reloads the current parameter values from the Tx and, if connected, the receiver.

#### stats; #### 
Starts streaming statistics. Terminate by sending any character. Format:

<table>
    <tr>
        <td>Tx LQ</td><td>Tx valid frames LQ</td><td>Rx LQ</td>
        <td>Tx RSSI</td><td>Rx RSSI</td><td>Tx SNR</td>
        <td>Tx bytes/sec transmitted</td><td>Tx bytes/sec received</td>
    </tr>
</table>

#### listfreqs; #### 
Lists the frequencies used in the FHSS scheme.

#### systemboot; #### 
Invokes the system bootloader.

### Tx modules with an ESP WiFi bridge ###

#### esppt; #### 
Enters the serial passthrough mode (communication between CLI port and the Serial port).

#### espboot; #### 
Reboots a ESP32 module and enters the serial passthrough mode. For flashing the ESP32 module through the CLI port.

### Tx modules with an HC-04 Bluetooth module ###

#### hc04 pt; #### 
Enters the serial passthrough mode (communication between CLI port and the Serial port).

#### hc04 setpin; #### 
Set the pin of the HC-04 module.