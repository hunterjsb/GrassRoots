![y](https://3023500.fs1.hubspotusercontent-na1.net/hub/3023500/hubfs/logos/super-sod-logo.png?width=245&name=super-sod-logo.png)
# API Documentation ![Python](https://img.shields.io/badge/Version-0.1.0-magenta?logo=python&style=flat)

## Contents
- [`Making a Request`](#Request)
  - [`Heaaders`](#headers)
  - [`Attributes`](#json-payload)
  - [`Example`](#example)
- [`Response`](#commands)
  - [`Status Codes`](#status-code)
  - [`Attributes`](#response-json)
  - [`Example`](#response-example)
***

## Endpoint: `/api/availability`

### Description

This endpoint checks the availability of specific sod varieties in a given zipcode and with minimum quantities.

### Request

#### Method

`POST`

#### Headers

- `Authorization: Bearer YOUR_API_TOKEN`

#### JSON Payload

- `zip` (integer, required): The zipcode to check the availability in. 
- `varieties` (array, required): A list of the following:
  - `sku` (integer, required): the variety's SKU
  - `quantity` (integer, required): the quantity of that SKU
- `fulfillmentType` (string, optional): the way in which the order should be fulfilled. If `fulfillmentType` is not provided, it defaults to `"standard`". Possible values are `"standard"`, `"pickup"`, `"beforeNine"`, and `"beforeNoon"`.

#### Example
```bash
POST /api/availability
```

```json
{
  "zip": 12345,
  "fulfillmentType": "pickup",
  "varieties": [
    {
      "sku": 1,
      "quantity": 25
    },
    {
      "sku": 2,
      "quantity": 30
    }
  ]
}

```
---
### Response

#### Status codes
- `200 OK`: The request was successful, and the availability data is returned.
- `400 Bad Request`: The request is malformed or missing required information.
- `401 Unauthorized`: The API token provided is invalid or missing.

#### Response JSON
- `status` (string): The status of the request, either "success" or "error".
- `error` (string, optional): A descriptive error message if the request failed.
- `data` (array, optional): An array of objects containing the availability data for each request item if the request was successful.
  - `dates` (array of strings): An array of available dates in the "yyyy-mm-dd" format.
  - `message` (string): A message to display to the user.
  - `exendedCalendar` (boolean): Whether or not the calendar should be extended.

#### Response Example
```json
{
  "status": "success", 
  "error": null,
  "data":
    {
      "dates": ["2023-05-03", "2023-05-04", "2023-05-05", "2023-05-06", "2023-05-08", "2023-05-09", "2023-05-10", "2023-05-11"], 
      "message": "Sod variety is available on thelisted dates.",
      "extendedCalendar": false
    }
}

