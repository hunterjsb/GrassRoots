![y](https://3023500.fs1.hubspotusercontent-na1.net/hub/3023500/hubfs/logos/super-sod-logo.png?width=245&name=super-sod-logo.png)
# API Documentation ![Python](https://img.shields.io/badge/Version-0.0.1-blue?logo=python&style=flat)

## Contents
- [`Making a Request`](#Request)
  - [`Heaaders`](#headers)
  - [`Payload`](#json-payload)
  - [`Example`](#example)
- [`Response`](#commands)
  - [`Status Codes`](#status-code)
  - [`Response JSON`](#response-json)
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
- `quantity` (integer, required): The minimum quantity available.
- `varieties` (array, required): A list of the following:
  - `sku` (integer, required): the variety's SKU
  - `quantity` (integer, required): the quantity of that SKU

#### Example
```bash
POST /api/availability
```

```json
{
  "zip": 12345,
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

#### Response Example
```json
{
  "status": "success",
  "error": null,
  "data": [
    {
      "dates": [
        "2023-04-01",
        "2023-04-02",
        "2023-04-03"
      ],
      "message": "Sod variety 1 is available on the listed dates."
    },
    {
      "dates": [
        "2023-04-04",
        "2023-04-05",
        "2023-04-06"
      ],
      "message": "Sod variety 2 is available on the listed dates."
    }
  ]
}

