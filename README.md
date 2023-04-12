# GET Diagnostic and OEM Info

Returns the diagnostif info (if exists) along with OEM info for given VIN.


## Headers

* `api_key`: <your_api_key>

## Request

The following query parameters are available.

| **Name**                         | **Type**         | **Presence** | **Example**     | **Description**                                                                                                                    |
| -------------------------------- | ---------------- | ------------ | --------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| VIN                       | string              | required     |     SJNFAAZE1U0077476 | Vehicle VIN to lookup                                                                               |


## Response Body

A response contains the diag and OEM info for vehicle.
The following table lists the available `attributes`:

| **Name**                               | **Type**      | **Example**                            | **Description**                                                                                                                                                                                                                     |
| -------------------------------------- | ------------- | -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Moba document URL                                    | URL        | https://certificate.get-moba.com/certificates/c7acd7169b4.pdf | Direct link to check the Moba digital certificate                                                                                                                                  |
| Token                                   | string        | "c7acd7169b4"                                  | Moba certificate unique access code                                                                                                                                                                  |
| Date of issue                   | string        | "20211112"                                  | Day, month, year the certificate has been performed                                                                                                                                                                                      |
| Brand                                  | string        | "Nissan"                                 | Brand name                                                                                                                                                                                                                          |
| model                                  | string        | "Leaf 40 kWh"                                 | Model and version name                                                                                                                                                                                                                          |
| SOH                                | Integer        | 93%                      | State of Health in % (based on OEM standards)                                                                                                                    |
| Mileage                    | Integer         | 29129 km                                | Mileage in km / mile                                                                                                                                                                                                          |
| Battery Warranty                             | string       | "5 years - 100 000 km"                                    | OEM Battery Warranty: Years - mileage                                                                                                                                                                        |
| Curb weight     | string | 1558 kg      | ACurb weight in kg / lb                                                                                                                                                            |
| Gross Vehicule Weight         | string         | 1990 kg    | Gross vehicule weight in kg / lb                                                                                                                                                                                                                                                                                                      |
| Total Power    | string | 110 kW               | Total power in kW                                                                                                     |
| Maximal speed     | string | 144 km/h       | Maximal speed in km/h or mile/h                                                                                                                                                          |
| fullPackCapacity                      | string          | 40 kWh                                   | Full pack capacity when new in kWh |
| Usefull capacity        | string       | 38,40 kWh                                    | Usefull capacity when new in kWh                                                                                                                                                              |
| AC Charging Power (max)               | stirng         | 6,6 kW                                 | AC charging power (max) in kW                                                                                                                                                   |
| DC Charging Power (max)              | string       | 50 kW                                  | DC charging power (max) in kW                                                                                                                                           |
|AC Charging Type | string    | Quick Charge Port  | AC charging connector type                                                                                                                                                           |
| DC Charging Type      | string| CHAdeMO connector                   | DC charging connector type                                                                                                                                  |
|AC Charge range | string    | 0% - 100%                                  | AC charge range in %                                                                                                                                                           |
|DC Charge Range | string    | 20% - 80%                                   | DC charge range in %                                                                                                                                                           |
|AC Charge time | string    | 7h30                                   | AC charge time in h                                                                                                                                                           |
|DC Charge time | string    | 1h00                                   |DC Charging time in h                                                                                                                                                          |
|Vehicule consumption | string    | 148 Wh/km                                  |Vehicule consumption Wh/km or Wh/mile                                                                                                                                                          |
|OEM range | string    |378 km                                  |OEM range in km / mile                                                                                                                                                          |
| NEDC/WLTP | string    | NEDC                                   |OEM Driving cycle standard                                                                                                                                                          |

## Example

### Request

```http
GET http://api.app-moba.com/miner/api.php?action=getBible&VIN=SJNFAAZE1U0077476
Api-Key: my-secret-key
```

### Response

#### 200 Ok

Body:
```json
{
    "diag": {
        "VIN": "SJNFAAZE1U0077476",
        "BatteryAmps": -0.24,
        "soh": 97,
        "soc": 97.4,
        "accVolts": 11.6259765625,
        "voltage": 401.82,
        "hx": 286.72,
        "odometer": 2908,
        "BMSserial": "230UK11985000251",
        "BMSv1": "5SH2D",
        "BMSv2": "0",
        "capacityAH": 41.53,
        "qc": 1,
        "l0l1l2": 42,
        "vcells": "0",
        "tc1": 6,
        "tc3": 255,
        "tc4": 4,
        "tc5": 4,
        "shunt1": "0",
        "shunt2": "ffffffff",
        "shunt3": "0",
        "range": 63,
        "link": "http://127.0.0.1:8888/miner/_connector/certificates/99fe5387ff.pdf",
        "version": "24 kWh",
        "date_immat": "20190927",
        "modele": "NISSAN|LEAF (24 / 30 kWh)",
        "QuickCh": 1,
        "NormalCh": 42,
        "re_BMS": "Yes",
        "guarantee_V2": "5 years - 100 000 km",
        "guarantee_V2_year": 5,
        "guarantee_V2_km": 100000,
        "tauxdecharge": "2%",
        "name": "Nissan Leaf 24 kWh"
    },
    "oem": {
        "marque": "Nissan",
        "modele": "Leaf",
        "version": "24 kWh",
        "curbWeight": "1525",
        "grossVehicleWeight": "1965",
        "totalPower": "80",
        "maximalSpeed": "145",
        "fullPackCapacity": "24",
        "usefulCapacity": "24",
        "acChargingPower": "6,6",
        "dcChargingPower": "50",
        "acChargeRangeLow": "0%",
        "acChargeRangeHigh": "100%",
        "acChargeTime": "4h00",
        "dcChargeRangeLow": "0%",
        "dcChargeRangeHigh": "80%",
        "dcChargeTime": "0h30",
        "vehicleConsumption": "173",
        "oemRange": "190",
        "wltp/nedc": "NEDC"
    }
}
}
```

##### 404 NOT FOUND

VIN not found

```json
{
    "err": "VIN Not found"
}
```

##### 403 Forbidden

* API-Key is missing
* API-Key is invalid
* API-Key not authorized to perform action

```json
{
    "error": true,
    "message": "Access Denied. Invalid Api key"
}
```
