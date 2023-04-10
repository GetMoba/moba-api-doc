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
| Token                                   | String        | "c7acd7169b4"                                  | Moba certificate unique access code                                                                                                                                                                  |
| Date of issue                   | String        | "20211112"                                  | Day, month, year the certificate has been performed                                                                                                                                                                                      |
| Brand                                  | String        | "Nissan"                                 | Brand name                                                                                                                                                                                                                          |
| model                                  | String        | "Leaf 40 kWh"                                 | Model and version name                                                                                                                                                                                                                          |
| SOH                                | Integer        | 93%                      | State of Health in % (based on OEM standards)                                                                                                                    |
| Mileage                    | Integer         | 29129 km                                | Mileage in km / mile                                                                                                                                                                                                          |
| Battery Warranty                             | Hash       | 3                                      | OEM Battery Warranty: Years - mileage                                                                                                                                                                        |
| Curb weight     | string | 1558 kg      | ACurb weight in kg / lb                                                                                                                                                            |
| Gross Vehicule Weight         | string         | 1990 kg    | Gross vehicule weight in kg / lb                                                                                                                                                                                                                                                                                                      |
| Total Power    | string | 110 kW               | Total power in kW                                                                                                     |
| Maximal speed     | string | 144 km/h       | Maximal speed in km/h or mile/h                                                                                                                                                          |
| fullPackCapacity                      | string          | 40 kWh                                   | Full pack capacity when new in kWh |
| Usefull capacity        | string       | 38,40 kWh                                    | Usefull capacity when new in kWh                                                                                                                                                              |
| dc_charging_curve.power                | Float         | 200.0                                  | power level at the given percentage in kW                                                                                                                                                                                           |
| dc_default_charging_curve              | Boolean       | false                                  | `true` if the charging curve is based on the default curve instead of real measured data.                                                                                                                                           |
| energy_consumption.average_consumption | Float         | 15.4                                   | in kWh/100km. Usually the WLTP value.                                                                                                                                                                                               |
| dc_charge_ports                        | Array<String> | ["ccs","tesla_ccs"]                    | All DC charge ports, that the vehicle is capable to charge with. Possible values: `ccs`, `chademo`                                                                                                                                  |


## Example

### Request

```http
GET http://localhost:8888/miner/api.php?action=getBible&VIN=SJNFAAZE1U0077476
Api-Key: my-secret-key
```

### Response

#### 200 Ok

Body:
```json
{
    "diag": {
        "UID": "c89d19c22196c04f643e07bbd1595d4c",
        "time": 1613027290,
        "canbus": "Nissan Leaf (40 kWh)",
        "cmd": "@LBB",
        "rented": "No",
        "dongle": "BFP_00000026",
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
        "tc2": "??",
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
        "entity": "143",
        "modele": "NISSAN|LEAF (24 / 30 kWh)",
        "QuickCh": 1,
        "NormalCh": 42,
        "scoreLBB": false,
        "capacityah": null,
        "bmsv1": null,
        "bmsv2": null,
        "bmsserial": null,
        "re_BMS": "Yes",
        "kw": 0,
        "guarantee_V2": "5 years - 62 000 km",
        "guarantee_V2_year": 5,
        "guarantee_V2_km": 100000,
        "newmodel": "NISSAN LEAF 24 KWH",
        "VehiculeID": "Nis_Leaf_24kw_8",
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
        "acChargeRange": "0% - 100%",
        "acChargeTime": "4h00",
        "dcChargeRange": "0% - 80%",
        "dcChargeTime": "0h30",
        "vehicleConsumption": "173",
        "oemRange": "190",
        "wltp/nedc": "NEDC"
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
