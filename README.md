Audio preamplifier control software
===================================

This is an application for controlling a stereo audio preamplifier. Items covered include
*  Source selection
*  Volume control
*  Mute
*  Visual display of above settings
*  Storage of current settings

An ESP32-DevKitC V4 interfaces through a motherboard to the on-board rotary encoder, IR receiver and 320x240 TFT display. External interfaces connect to a source select relay board and balanced digital volume controller / preamplifier board (based on Bruno Putzeys balanced pre-amp with an integrated MAS6116 digital volume control chip).

The Quadrature rotary encoder/switch (PEC11R) provides control of the volume as the default mode. Pressing the encoder shaft button switches over to SOURCE SELECT mode and this remains as the active mode till rotary encoder turning is inactive for longer than the TIME_EXITSELECT value (in seconds).

An Infra-red receiver module (TSOP4836) provides remote control of volume level, balance, mute, source select and display on/off. RC5 protocol was chosen as I had a remote transmitter from my existing preamplifier using that code. It's also the protocol used by many freely available transmitters.

The MUSE72323 stereo digital volume control provides independently programmable gain of each channel from -111.75dB to 0dB together with mute. Communication between the ESP32 and the MUSE72323 is via an SPI bus.

The 320x240 TFT display with an SPI interface provides visual data for source input selected, atten setting (-111.75dB to 0dB) and mute status. It also includes a clock.

Additional functionality is provided by use of the ESP32's built-in peripherals. These are
* WiFi remote control of volume, source selection and mute
* Clock (locked to internet NTP server)
* OTA software update capability

Code Libraries
=================
Interfacing with the TFT display, source selector, IR decoder, rotary encoder/switch, WiFi and NTP uses shared libraries. These are
* TFT_eSPI (PlatformIO libdeps value = bodmer/TFT_eSPI@^2.3.70)
* RC5    https://github.com/guyc/RC5
* ESP32RotaryEncoder (PlatformIO libdeps value = maffooclock/ESP32RotaryEncoder@^1.1.0)
* MCP23S08 SPI bus expander for source selector (PlatformIO libdeps value = robtillaart/MCP23S08@^0.4.0)
* MUSES72323    https://github.com/GeoffWebster/Muses72323
* https://github.com/me-no-dev/ESPAsyncWebServer.git
* ArduinoJson
* ayushsharma82/ElegantOTA@^3.1.0