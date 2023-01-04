# localtuya-device-datapoints
List of data points for various Tuya devices, required to setup localtuya integration.

Data points can be obtained by 
1. logging into the Tuya IoT Platform
2. Select '**Cloud**' > '**Development**' from the menu
3. Select your project
4. Goto '**Devices**'
5. Click **Debug device** in the *Operations* column
6. Select 'Device Logs' tab
7. Open the browser Developer Tools (F12) and open the Network tab
8. Select a DP from the 'Select DP ID' dropdown
9. Hit 'Search'

In the background a network request will be done, available as list in the network calls overview. Select that request and open the 'Payload' tab.

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

The `"code"` value is your DP ID. In this case `2`, which translates to the `'Switch 2'` the relay for socket #2 of the SHP5 smart socket.


## Blitzwolf SHP5

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
| 22  | Voltage coe        |              |
| 23  | Electric coe       |              |
| 24  | Power coe          |              |
| 25  | Electricity coe    |              |
| 26  | Fault              |              |

> **Add Electricity** = Power consumption since last report

## Blitzwolf SHP7

| DP  | Description        | Value          |
| --- | ------------------ | -------------- |
| 1   | Switch 1           | {true,false}   |
| 7   | Switch 2 (USB)     | {true,false}   |
| 9   | Countdown Switch 1 | 0-86400 s      |
| 10  | Countdown Switch 2 | 0-86400 s      |
| 17  | Add Electricity*   | 0-50000 kWh    |
| 18  | Current            | 0-30000 mA     |
| 19  | Power              | 0-5000 W       |
| 20  | Voltage            | 0-50000 V      |
| 21  | Test bit           |                |
| 22  | Voltage coe        |                |
| 23  | Electric coe       |                |
| 24  | Power coe          |                |
| 25  | Electricity coe    |                |
| 38  | Relay Status       | { "power_off", "power_on",  "last" } |
| 39  | Indicator Light      | { "none", "relay", "pos" } |
| 40  | Child Lock           | {true,false} |
| 41  | Cycle Time           |              |
| 42  | Random Time          |              |
| 43  | Inching Switch       |              |

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
