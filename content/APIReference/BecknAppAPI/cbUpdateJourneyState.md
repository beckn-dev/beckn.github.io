---
title: "Update Journey State - Callback"
---

BA receives Journey object with updated Journey state as callback.

#### API Endpoint:

    Journey/State/cb_update

#### Request Structure :

The request structure of a search request consists of a **Header** and **Body**.

The request Header is an object of the [Header](/Resources/Header) class. The *Action* field of the Header object will be equal to *"Journey/State/cb_update"*

The request Body is a [Journey](/Resources/Journey) object with the state updated.

##### Example Request:

**Header :**

```json
{
  "Action": "Journey/State/cb_update",
  "Token": "string",
  "transactio_id" : "string",
  "Timestamp": "2019-09-13T14:31:54",
  "message" : "SUCCESS"
}
```
**Body :**

```json
{
  "id" : "< Unique Journey ID >",
  "state" : "NEW STATE",
  "origin": {
    "location": {
      "value": "(12.878742,77.999654)",
      "format": "geocode"
    },
    "departure_time": {
      "value": "2019-09-13T14:31:54+05:30",
      "format": "utc"
    }
  },
  "destination": {
    "location": {
      "value": "(12.454612,77.876287)",
      "format": "geocode"
    }
  },
  "state": "INIT",
  "trips": [
    {
      "id": "< Unique Trip ID >",
      "travelers" : [
        {
          "profile" : {
            "first_name" : "John",
            "last_name" : "Doe",
            "phone" : "+91-8899889988",
            "email" : "john.doe@example.com"
          },
          "cred" : {
            "type" : "aadhaar",
            "format" : "jpeg",
            "encoding" : "base64",
            "data" : "51o2POfNqXeZ..."
          }
        }
      ],
      "MobilityService": {
        "id": "h3nM51o2POfNqXeZJXu6",
        "name": "Port Authority Bus Service",
        "provision_type": "FIXED",
        "reservability": {
          "is_reservable": true
        },
        "capacity_type": {
          "carrier_reservable": false,
          "seat_reservable": false
        },
        "mobility_form": {
          "carrier": {
            "category": "BUS"
          },
          "medium": "ROADWAYS"
        }
      },
      "route": {
        "flexibilty": "FIXED CORRIDOR",
        "medium": "ROADWAYS",
        "stops": [
          {
            "location": "geocode:(12.878742,77.999654)@coord.(DD.DDDDDD);Vesey Street@name",
            "arrival_time": "2019-09-13T14:31:54+05:30",
            "buffer_time": "60 s",
            "departure_time": "2019-09-13T14:31:54+05:30"
          },
          {
            "location": "geocode:(12.878742,77.999654)@coord.(DD.DDDDDD);Fulton Street@name",
            "arrival_time": "2019-09-13T14:31:54+05:30"
          }
        ],
        "edges": [
          {
            "travel_time": "2 min",
            "path": "polyline:(12.878742,77.999654),(12.878742,77.999654),(12.878742,77.999654)"
          }
        ]
      }
    },
    {
      "id": "< Unique Trip ID >",
      "service": {
        "id": "Dl9jAJzRlCZirt8IJYwA",
        "name": "New York Subway",
        "provision_type": "FIXED",
        "reservability": {
          "is_reservable": true
        },
        "capacity_type": {
          "carrier_reservable": false,
          "seat_reservable": false
        },
        "mobility_form": {
          "carrier": {
            "category": "TRAIN"
          },
          "medium": "RAILWAYS"
        }
      },
      "route": {
        "flexibilty": "FIXED CORRIDOR",
        "medium": "RAILWAYS",
        "stops": [
          {
            "location": "station:33rd Street, World Trade Center@name",
            "arrival_time": "2019-09-13T14:31:54+05:30",
            "buffer_time": "60 s",
            "departure_time": "2019-09-13T14:31:54+05:30"
          },
          {
            "location": "station:34th Street, Pennsylavania Station@name",
            "arrival_time": "2019-09-13T14:31:54+05:30"
          }
        ],
        "edges": [
          {
            "travel_time": "12 min",
            "path": "polyline:(12.878742,77.999654),(12.878742,77.999654),(12.878742,77.999654)"
          }
        ]
      }
    }
  ],
  "transfers": [
    {
      "origin": "geocode:(12.878742,77.999654)@coord.(DD.DDDDDD);Fulton Street@name",
      "destination": "station:33rd Street, World Trade Center@name",
      "medium": "ROADWAYS",
      "mode": "WALK",
      "time": "5 min"
    }
  ]
}
```

#### Response Structure

The response structure will consist of a **Header** and an optional **Body**

As the API is non-blocking, the Response to the above Request will be a simple **ACK** or a **NACK** response. The response Header is an object of the [Header](/Resources/Header) class. The ACK and NACK response Headers will have the action field equal to *"ACK"* and *"NACK"* respectively. The ACK response Body will be an **empty** JSON object.

The NACK response body may optionally contain an [Error](/Resources/Error) object.

##### Example ACK Response

**Header :**

```json
{
  "action": "ACK",
  "message": "Success Message string"
}
```

**Body :**
``` json
{}
```
##### Example NACK Response :

**Header :**
```json
{
  "action": "NACK",
  "message": "Error message string"
}
```
**Body :**
```json
{}
```
