# API Documentation

## Endpoint: `/api/availability`

### Description

This endpoint checks the availability of specific sod varieties in a given zipcode and with minimum quantities.

### Request

#### Method

`GET`

#### Headers

- `Authorization: Bearer YOUR_API_TOKEN`

#### Query Parameters

- `zip` (integer, required): The zipcode to check the availability in.
- `quantity` (integer, required): The minimum quantity available.
- `varieties` (string, required): A comma-separated list of sod variety IDs.

#### Example

```bash
GET /api/availability?zip=12345&quantity=50&varieties=1,2
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

