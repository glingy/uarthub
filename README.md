# UART Hub

This is a 6-port "null modem cable". There are six 4-signal UART channels with flow control. Each channel is connected to all six RP2040's at each USB port to allow full software configuration of which USB ports communicate on which channels. 

For example with the following configuration:
```
Channel 0: Port 0, Port 1
Channel 1: Port 0, Port 2
Channel 2: Port 1, Port 3
Channel 3: Port 1, Port 2
Channel 4: Port 0, Port 1
Channel 5: Port 0, External
```

A computer connected to USB 0 will see four USB CDC-ACM serial ports (COM ports on Windows, TTY's on Linux). They will be connected to USB 1, USB 2, USB 1, and the external pins labeled `5` respectively. Port 1 will also have four serial ports (USB 0, USB 3, USB 2, USB 0). Note that in this case there are two independent serial connections between USB 0 and 1. USB 2 will have two serial ports, USB 3 will only see one port, and USB 4 & 5 will see no serial ports. 

USB 0 will also have an additional management serial port that allows runtime configuration of which ports are associated with each channel via a terminal-based UI.

This project is not intended to work for other protocols (I2C, SPI), but the hardware should be capable of supporting I2C or SPI devices on the external pins, the RP2040 uses the same pins for I2C/SPI as it does for UART. 