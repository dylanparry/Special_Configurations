# Marlin_Configurations
In this repository there are the configuration files for several Marlin firmware features for the Ender3 V2/S1 printer, the main
project files are in the firmware repository: https://github.com/mriscoc/Ender3V2S1

### These special configurations and releases are sponsored by donors.

For have a special build you must to provide a config json with only your personal choices, for example: for get a
special build that have a hotend volcano, bltouch and 4.2.2 board it is necessary only write a Volcano.json with this content:

```json
{
"Configuration_adv.h" : [
],
"Configuration.h" : [
  {
    "op": "CustomVal",
    "searchfor": "TEMP_SENSOR_0",
    "value": "5",
    "comment": "Volcano thermistor"
  },
  {
    "op": "CustomVal",
    "searchfor": "HEATER_0_MINTEMP",
    "value": "5",
    "comment": "Volcano thermistor"
  },
  {
    "op": "CustomVal",
    "searchfor": "HEATER_0_MAXTEMP",
    "value": "300",
    "comment": "Volcano thermistor"
  }
],
"Version.h" : [
]   
}
```

Then, request to the `CreateConfigs.py` to build a configuration with `CreateConfigs.Generate('', ['422','BLTouch','Volcano'])`; the last "Volcano" will overwrite the necessary values in the configuration file.

~~The above can be done using a GUI by running the `zen-configurator.py` script. The script requires Python (tested with 3.9.5+) to have been installed with TKInter (Tcl/Tk). Simply check the boxes with the configs you want to add (you can verify what the configs add by looking at the json files that match the name of the checkboxes) and click Create Configuration. This will happen in the background and will be present in a config folder in the same directory called "Custom-zenUI." Progress will be shown in standard output which is directed to the text box. If you need to debug the script and no errors show because the window closed, edit the script and comment out the `text.start()` line (line 109).

The `CreateConfigs.py` script supports five basic operations over the configuration files:

> **InsertAfter**: allows to insert text after match a given mask.  
> **Custom**: allows to replace text  after match a given mask.  
> **CustomVal**: allows to replace numeric values.  
> **Enable**: allows to enable a feature.  
> **Disable**: allows to disable a feature.  
> **Replace**: allows to replace a mask with other text.

For example to change the default tramming points you can write in the "Configuration_adv.h" section of the json the command:
```json
  {
    "op": "Custom",
    "searchfor": "TRAMMING_POINT_XY",
    "mask": "{.*}",
    "value":"{ { 29, 29 }, { 299, 29 }, { 299, 299 }, { 29, 299 } }"
  }
```

For disable Multiple probing you can write in the "Configuration.h" section of the json the command:
```json
  {
    "op": "Disable",
    "searchfor": "MULTIPLE_PROBING",
    "comment": "Custom disable"
  }
```
The comment line is optional. Masks are in regex format, use the provided json as examples.

## Donations
Thank you for your support, I receive donations through [Patreon](https://www.patreon.com/mriscoc) and [Paypal](https://www.paypal.com/paypalme/mriscoc)   

[<img src="https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif">](https://www.paypal.com/donate?business=85SPAAR6UZEE8&currency_code=USD)

# Disclaimer
THIS FIRMWARE AND ALL OTHER FILES IN THE DOWNLOAD ARE PROVIDED FREE OF CHARGE WITH NO WARRANTY OR GUARANTEE. SUPPORT IS NOT INCLUDED JUST BECAUSE YOU DOWNLOADED THE FIRMWARE. WE ARE NOT LIABLE FOR ANY DAMAGE TO YOUR PRINTER, PERSON, OR ANY OTHER PROPERTY DUE TO USE OF THIS FIRMWARE. IF YOU DO NOT AGREE TO THESE TERMS THEN DO NOT USE THE FIRMWARE.

# LICENSE
For the license, check the header of each file, if the license is not specified there, the project license will be used. Marlin is licensed under the GPL.
