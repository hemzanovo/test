Bandwidth
=======

## get bandwidth
Get bandwidth usage data for a server

/bandwidth/{serverTag}

Parameters


| Name        | Description           
| ------------- |:-------------:|
| period     | Number of days to fetch data for, defaults to 35 | 
| start     | Timestamp for the start of the requested period     | 
| end | Timestamp for the end of the requested period      | 

**example succesful operation**
 ``` json
 {
  "data": {
    "2020-05-08": {
      "in": 230.745,
      "out": 231.232,
      "tot": 461.977
    },
    "2020-05-09": {
      "in": 230.745,
      "out": 231.232,
      "tot": 461.977
    }
  },
  "monthly": {
    "2020-05": {
      "in": 1230.745,
      "out": 1231.232,
      "tot": 2461.977
    },
    "2020-06": {
      "in": 330.745,
      "out": 231.232,
      "tot": 561.977
    }
  }
}
 ```

Servers
=======
## get server information by tag

/servers/{serverTag}

**succesful operation**
``` json
{
  "location": {
    "dataCenter": "Delft (TDCG)",
    "rack": "2.C Row F 10",
    "unit": 40,
    "rackId": 4411
  },
  "hardwareProfile": "123-123"
}
```


