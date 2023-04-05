# API Documentation

## Endpoint: `/api/availability`

### Description

This endpoint checks the availability of a specific sod variety in a given zipcode and with a minimum quantity.

### Request

#### Method

`POST`

#### Headers

- `Content-Type: application/json`
- `Authorization: Bearer YOUR_API_TOKEN`

#### Body

- `zip` (integer, required): The zipcode to check the availability in.
- `variety` (integer, required): The sod variety ID.
- `quantity` (integer, required): The minimum quantity available.

#### Example

```json
{
  "zip": 12345,
  "variety": 1,
  "quantity": 50
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
- `data` (object, optional): Contains the availability data if the request was successful.
  - `dates` (array of strings): An array of available dates in the "yyyy-mm-dd" format.
  - `message` (string): A message to display to the user.

```json
{
  "status": "success",
  "error": null,
  "data": {
    "dates": [
      "2023-04-01",
      "2023-04-02",
      "2023-04-03"
    ],
    "message": "Sod variety is available on the listed dates."
  }
}
```
