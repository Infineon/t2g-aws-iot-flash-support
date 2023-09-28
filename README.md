<img src="./images/IFX_LOGO_600.gif" align="right" width="150"/>

# AWS IoT Over-the-Air (OTA) Update Support for T2G
**This library provides some functionalities which enable the OTA operation on T2G series MCU kits.**

## Functions

**Flash access interface**
<br>A library [aws-iot-device-sdk-port](https://github.com/Infineon/aws-iot-device-sdk-port) which is used to let [AWS IoT Device SDK for Embedded C](https://github.com/aws/aws-iot-device-sdk-embedded-C) work on Infineon MCUs requires some external functions to store the received firmware during the OTA session. This library provides the functions as follows:<br>
<table border="1" style="border-collapse: collapse">
<thead><tr>
<th>Function</th><th>Overview</th></tr></thead>
<tbody>
<tr><td><code>flash_area_open()</code></td><td>Opens the area for use. The configuration of the areas should be prepared outside of this library as <i>boot_area_descs</i>. This library refers it to perform its functionality. Typically, the configuration has two areas as primary and secondary; the secondary bank is specified as the inactive bank of Code Flash memory operating in a dual bank configuration.</td></tr>
<tr><td><code>flash_area_close()</code></td><td>Closes the area after its use.</td></tr>
<tr><td><code>flash_area_read()</code></td><td>Reads <i>len</i> bytes of flash memory at <i>off</i> to the buffer at <i>dst</i>.</td></tr>
<tr><td><code>flash_area_write()</code></td><td>Writes <i>len</i> bytes of flash memory at <i>off</i> from the buffer at <i>src.</i></td></tr>
<tr><td><code>flash_area_erase()</code></td><td>Erases <i>len</i> bytes of flash memory at <i>off</i>.</td></tr>
</tbody>
</table>

**OTA status marking**
<br>OTAs in a dual-bank configuration must have information to determine which bank to activate. This library provides the functions as follows:<br>
<table border="1" style="border-collapse: collapse">
<thead><tr>
<th>Function</th><th>Overview</th></tr></thead>
<tbody>
<tr><td><code>boot_set_pending()</code></td><td>In this implementation, the location to store the info is Work Flash of T2G MCU. This function sets that flash marker to make next boot up use the current inactive bank as the active bank.</td></tr>
<tr><td><code>boot_set_confirmed()</code></td><td>Essentially, this function is called to write some mark that the new firmware has been verified. But in this implementation, the verification of the firmware is expected to done with digital signature during its boot sequence, so this function is not implemented (just declared and always returns success).</td></tr>
</tbody>
</table>

**Other declared items**
<br>There are several other definitions and symbols available in addition to the above, but these are only to make the aws-iot-device-sdk-port library available (to get the build through and work properly), and do not provide functionality.


## Dependencies  
If the application specifies as use this library, other libraries listed below will be automatically included in the project:
- [mqtt](https://github.com/Infineon/mqtt)
- [retarget-io](https://github.com/Infineon/retarget-io)

## References  

ModusToolbox™ is available online:
- <https://www.infineon.com/modustoolbox>

Associated TRAVEO™ T2G MCUs can be found on:
- <https://www.infineon.com/cms/en/product/microcontroller/32-bit-traveo-t2g-arm-cortex-microcontroller/>

More code examples can be found on the GIT repository:
- [TRAVEO™ T2G Code examples](https://github.com/orgs/Infineon/repositories?q=mtb-t2g-&type=all&language=&sort=)

For additional trainings, visit our webpage:  
- [TRAVEO™ T2G trainings](https://www.infineon.com/cms/en/product/microcontroller/32-bit-traveo-t2g-arm-cortex-microcontroller/32-bit-traveo-t2g-arm-cortex-for-body/traveo-t2g-cyt4bf-series/#!trainings)

For questions and support, use the TRAVEO™ T2G Forum:  
- <https://community.infineon.com/t5/TRAVEO-T2G/bd-p/TraveoII>  
