# LocalTuya Device Datapoints

> *Notes:*  
> A [Tuya IoT ](https://iot.tuya.com/) project **must** be created for this to work  
> Tuya device authorization can expire, which will result in errors in Home Assistant
> (Presumably) the Tuya app on the smart phone needs to be closed for this process to work reliably

Early 2023, adding/configuring Tuya devices in the Home Assistant [LocalTuya](https://github.com/rospogrigio/localtuya) community add-on is (still) a rather confusing process. Adding a device involves manually configuring the Data Points, which are the properties like relays and power consumption a Tuya device exposes through its local API.  

These properties do not advertise themselves as a friendly name or data type, but as numbers. Finding what property these DPs represent is quite cumbersome, hence I created this repo to remind me of this process and also include the DPs for several of my Tuya devices to save future me from having to look them up (again).

> **2023-01-04**:
> I found and included a table containing known [🔗DPs for Tuya v3.3 devices](#tuya-v33-dps)

## Obtaining data points for your Tuya device

1. Login to the [Tuya IoT Platform](https://iot.tuya.com/)
2. Select '**Cloud**' > '**Development**' from the menu
3. Select your project
4. Goto '**Devices**'
5. Click **Debug device** in the *Operations* column  
*💡 hidden if viewport is too narrow*
6. Select '**Device Logs**' tab
7. Open the browser Developer Tools (EDGE:F12) and open the Network tab
8. Select a DP from the '**Select DP ID**' dropdown
9. Hit '**Search**'

In the background a network request will be done, available as `'list'` in the network calls overview.  
Select that request and open the 'Payload' tab.

The payload will look similar to this:

```json
{
  "startRowId": "",
  "pageNo": 1,
  "pageSize": 10,
  "code": "2",
  "startTime": 1672692811363,
  "endTime": 1672865611364,
  "projectCode": "*****",
  "sourceId": "*****",
  "sourceType": "4",
  "deviceId": "*****",
  "pageStartRow": "",
  "region": "EU"
}
```

The `"code"` value is your DP ID. In this case `2`, which translates to the `'Switch 2'` the relay for socket #2 of the *Blitzwolf SHP7* smart socket.

Once the device has been selected, the flow will be like this:

![Get DataPoint ID from Tuya IoT portal device debug](media/get-dp-ids-from-tuya-iot-portal.png)

# Device DPs

> Some clarification of DPs:   
> **Add Electricity** = Power consumption since last report  
> **... coe** = ... coefficient

## Generic 2 Button Wall Switch

Advertised as **SWITCH2**

| DP  | Description        | Value        |
| --- | ------------------ | ------------ |
| 1   | Switch 1           | {true,false} |
| 2   | Switch 2           | {true,false} |
| 9   | Countdown Switch 1 | 0-86400 s    |
| 15  | Countdown Switch 2 | 0-86400 s    |

## Blitzwolf SHP2

> [BW-SHP2](media/blitzwolf_bw-shp2.jpg): Wifi Smart Socket 16A with power monitoring  
> Also sold as **Gosund SP1** and **Tecking SP22**

| DP  | Description      | Value                                |
| --- | ---------------- | ------------------------------------ |
| 1   | Switch           | {true,false}                         |
| 9   | Countdown Switch | 0-86400 s                            |
| 17  | Add Electricity* | 0-50000 kWh                          |
| 18  | Current          | 0-30000 mA                           |
| 19  | Power            | 0-5000 W                             |
| 20  | Voltage          | 0-50000 V                            |
| 21  | Test bit         |                                      |
| 22  | Voltage coe      | 0-1000000                            |
| 23  | Electric coe     | 0-1000000                            |
| 24  | Power coe        | 0-1000000                            |
| 25  | Electricity coe  | 0-1000000                            |
| 38  | Relay Status     | { "power_off", "power_on",  "last" } |
| 39  | Indicator Light  | { "none", "relay", "pos" }           |
| 40  | Child Lock       | {true,false}                         |
| 41  | Cycle Time       |                                      |
| 42  | Random Time      |                                      |
| 43  | Inching Switch   | ???                                  |

## Blitzwolf SHP5

> [BW-SHP5](media/blitzwolf_bw-shp5.jpg): Wifi Smart Socket 16A with power monitoring, has 2 USB ports that can be switched separate from the main socket.  
> Also sold as **Gosund SP112**

| DP  | Description        | Value        |
| --- | ------------------ | ------------ |
| 1   | Switch 1           | {true,false} |
| 7   | Switch 2 (USB)     | {true,false} |
| 9   | Countdown Switch 1 | 0-86400 s    |
| 15  | Countdown Switch 2 | 0-86400 s    |
| 17  | Add Electricity*   | 0-50000 kWh  |
| 18  | Current            | 0-30000 mA   |
| 19  | Power              | 0-5000 W     |
| 20  | Voltage            | 0-50000 V    |
| 21  | Test Bit           |              |
| 22  | Voltage coe        | 0-1000000    |
| 23  | Electric coe       | 0-1000000    |
| 24  | Power coe          | 0-1000000    |
| 25  | Electricity coe    | 0-1000000    |
| 26  | Fault              |              |

## Blitzwolf SHP7

> [BW-SHP7](media/bitzwolf_bw-shp7.jpg): Dual smart socket with power monitoring.  
> Also sold as **Gosund SP211**

| DP  | Description        | Value                                |
| --- | ------------------ | ------------------------------------ |
| 1   | Switch 1           | {true,false}                         |
| 2   | Switch 2           | {true,false}                         |
| 9   | Countdown Switch 1 | 0-86400 s                            |
| 10  | Countdown Switch 2 | 0-86400 s                            |
| 17  | Add Electricity*   | 0-50000 kWh                          |
| 18  | Current            | 0-30000 mA                           |
| 19  | Power              | 0-5000 W                             |
| 20  | Voltage            | 0-50000 V                            |
| 21  | Test bit           |                                      |
| 22  | Voltage coe        | 0-1000000                            |
| 23  | Electric coe       | 0-1000000                            |
| 24  | Power coe          | 0-1000000                            |
| 25  | Electricity coe    | 0-1000000                            |
| 38  | Relay Status       | { "power_off", "power_on",  "last" } |
| 39  | Indicator Light    | { "none", "relay", "pos" }           |
| 40  | Child Lock         | {true,false}                         |
| 41  | Cycle Time         |                                      |
| 42  | Random Time        |                                      |
| 43  | Inching Switch     |                                      |

## LSC Ceiling Lamp-RGBCW

> Also sold by Livarno (LIDL)

 | DP  | Description           | Value                                   |
 | --- | --------------------- | --------------------------------------- |
 | 1   | Switch                | {true,false}                            |
 | 21  | Mode                  | { "white", "colour", "scene", "music" } |
 | 22  | Brightness            | 0-1000                                  |
 | 23  | Colour Temperature    | 0-1000                                  |
 | 24  | Colour                | { h [0-360], s [0-1000], v [0-1000] }   |
 | 25  | Scene                 | *complex datamodel*                     |
 | 41  | Remote Control Switch | {true,false}                            |
 | 26  | Countdown             | 0-86400 s                               |
 | 28  | Debugger              | { h [0-360], s [0-255], v [0-255] }     |

## Generic Smoke Detector (WiFi)

| DP  | Description           | Value                       |
| --- | --------------------- | --------------------------- |
| 16  | Silence               | {true,false}                |
| 1   | Smoke Detection State | { "alarm", "normal" }       |
| 2   | Smoke Sensor          | 0-100                       |
| 11  | Fault Alarm           |                             |
| 14  | Battery Level State   | { "low", "middle", "high" } |
| 15  | Battery Level         | 0-100 %                     |
| 101 | User Test             |                             |

### CountdownObject

```json
{
  "unit": "s",
  "min": 0,
  "max": 86400,
  "scale": 0,
  "step": 1
}
```

### Scene Data (LED)

```json
{
  "scene_num": {
    "min": 1,
    "scale": 0,
    "max": 8,
    "step": 1
  },
  "scene_units": {
    "unit_change_mode": {
      "range": [
        "static",
        "jump",
        "gradient"
      ]
    },
    "unit_switch_duration": {
      "min": 0,
      "scale": 0,
      "max": 100,
      "step": 1
    },
    "unit_gradient_duration": {
      "min": 0,
      "scale": 0,
      "max": 100,
      "step": 1
    },
    "bright": {
      "min": 0,
      "scale": 0,
      "max": 1000,
      "step": 1
    },
    "temperature": {
      "min": 0,
      "scale": 0,
      "max": 1000,
      "step": 1
    },
    "h": {
      "min": 0,
      "scale": 0,
      "unit": "",
      "max": 360,
      "step": 1
    },
    "s": {
      "min": 0,
      "scale": 0,
      "unit": "",
      "max": 1000,
      "step": 1
    },
    "v": {
      "min": 0,
      "scale": 0,
      "unit": "",
      "max": 1000,
      "step": 1
    }
  }
}
```

## Neve X RFW Wireless Chronothermostat

> [Neve X RFW](media/neve_xrfw.webp): Wifi enabled wireless chronothermostat  
Platform: `climate`

| DP  | Description                 | Value                                   | LocalTuya configuration                                              |
| --- | --------------------------- | --------------------------------------- | -------------------------------------------------------------------- |
| 1   | Switch                      | {true,false}                            | N/A                                                                  | 
| 2   | Mode                        | {"manual","auto","temporary","holiday"} | HVAC Mode DP + HVAC Mode Set: manual/auto                            | 
| 3   | Working status              | {"off","heat","antifreeze"}             | HVAC Current ACtion DP + HVAC Current Action Set: heating/no_heating |
| 16  | Set temperature             | 0-1000000                               | Target Temperature                                                   |
| 24  | Current temperature         | 0-1000000                               | Current Temperature                                                  |
| 27  | Temperature calibration     | 0-1000000                               | N/A                                                                  |
| 32  | Holiday temperature         | N/A                                     | N/A                                                                  |
| 33  | Holiday mode days setting   | 0-3                                     | N/A                                                                  |
| 37  | Week program                | *complex datamodel*                     | N/A                                                                  |
| 39  | Reset factory settings      | {true,false}                            | N/A                                                                  |
| 40  | Child lock                  | {true,false}                            | N/A                                                                  |
| 42  | Remaining time              | 0-1440                                  | N/A                                                                  |
| 45  | Fault alarm                 | N/A                                     | N/A                                                                  |
| 101 | Temporary time              | 0-1440                                  | N/A                                                                  |
| 102 | Total Start-Up Time         | 0-1440                                  | N/A                                                                  |
| 103 | Antifreeze temperature      | 0-1000000                               | N/A                                                                  |
| 104 | Fine temperature adjustment | 0-1000000                               | N/A                                                                  |

---

## Tuya v3.3 DPs

List of DPs for Tuya v3.3 devices.  
Table contains the DPs that a device *may* expose. In general it is a useful lookup table to identify the DPs read by LocalTuya.

Source: 🔗 https://pypi.org/project/tinytuya/

| DP ID | Function Point     | Type    | Range Units                   |
| ----- | ------------------ | ------- | ----------------------------- |
| 1     | Switch 1           | bool    | {true,false}                  |
| 2     | Switch 2           | bool    | {true,false}                  |
| 3     | Switch 3           | bool    | {true,false}                  |
| 4     | Switch 4           | bool    | {true,false}                  |
| 5     | Switch 5           | bool    | {true,false}                  |
| 6     | Switch 6           | bool    | {true,false}                  |
| 7     | Switch 7/usb       | bool    | {true,false}                  |
| 9     | Countdown 1        | integer | 0-86400 s                     |
| 10    | Countdown 2        | integer | 0-86400 s                     |
| 11    | Countdown 3        | integer | 0-86400 s                     |
| 12    | Countdown 4        | integer | 0-86400 s                     |
| 13    | Countdown 5        | integer | 0-86400 s                     |
| 14    | Countdown 6        | integer | 0-86400 s                     |
| 15    | Countdown 7        | integer | 0-86400 s                     |
| 17    | Add Electricity    | integer | 0-50000 kw                    |
| 18    | Current            | integer | 0-30000 mA                    |
| 19    | Power              | integer | 0-50000 W                     |
| 20    | Voltage            | integer | 0-5000 V                      |
| 21    | Test Bit           | integer | 0-5 n/a                       |
| 22    | Voltage coeff.     | integer | 0-1000000                     |
| 23    | Current coeff.     | integer | 0-1000000                     |
| 24    | Power coeff.       | integer | 0-1000000                     |
| 25    | Electricity coeff. | integer | 0-1000000                     |
| 26    | Fault              | fault   | ov_cr                         |
| 38    | Power-on state     | setting | enum { off, on, memory }      |
| 39    | Overcharge Switch  | bool    | {true,false}                  |
| 40    | Indicator status   | setting | enum { none, on, relay, pos } |
| 41    | Child Lock         | bool    | {true,false}                  |
| 42    | UNKNOWN            |         |                               |
| 43    | UNKNOWN            |         |                               |
| 44    | UNKNOWN            |         |                               |
