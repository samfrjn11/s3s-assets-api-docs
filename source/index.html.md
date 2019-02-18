---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
 - php: PHP

toc_footers:
  - <a href='https://s3s.eu/bto/signup' target='_blank'>Sign Up for an Assets API Key</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Assets API! You can use our API to access S3S Assets API endpoints, which can give you more information on your order status, serial numbers, checklists, statistics and test results.

You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```php
<?php

$api_key = "YOUR_API_KEY";

$client = new GuzzleHttp\Client([
  'base_uri' => 'https://s3s.eu/api/v2/',
  'headers' => [
    'Authorization' => 'Bearer ' . $api_key,
    'Accept'        => 'application/json',
  ]
]);

?>
```

> Make sure to replace `YOUR_API_KEY` with your API key.

The Assets API uses API keys to allow access to the API. You can request an API key at our [BTO portal](https://s3s.eu/bto/signup).

The Assets API expects the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer API_KEY`

<aside class="notice">
You must replace <code>API_KEY</code> with your personal API key.
</aside>

# Assets
## Get All Assets

> To get all available assets, use this code:

```php
<?php

  $result = $client->request('GET', 'assets');

?>
```


> The above command returns JSON structured like this:

```json
{
    "available_assets": [
        "/api/v2/assets",
        "/api/v2/assets/checklists",
        "/api/v2/assets/checklists/{id}",
        "/api/v2/assets/orders",
        "/api/v2/assets/statistics",
        "/api/v2/assets/test_results/{id}",
    ],
    "status_code": 200
}
```

This endpoint retrieves all available assets to you.

### HTTP Request

`GET https://s3s.eu/api/v2/assets`

## Get a Specific Asset Endpoint

> To get a specific asset, use this code:

```php
<?php

  $client->request('GET', 'assets/checklists/123');

?>
```

> The above command will return JSON structured like this:

```json
{
    "data": [
        {
            "id": 123,
            "chassis_serial_number": "C123456789ABCDEF",
            "assembly_serial_number": "US.2018.213",
            "service_contract": {
                "data": {
                    "name": "Standard Warranty (3 years)",
                    "description": "3 Years Standard Warranty, advanced replacement is included.",
                    "duration": 3
                }
            },
            "status": "finished",
            "created_at": {
                "date": "2018-01-16 09:42:50.000000",
                "timezone_type": 3,
                "timezone": "Europe/Brussels"
            },
            "updated_at": {
                "date": "2018-01-16 14:31:49.000000",
                "timezone_type": 3,
                "timezone": "Europe/Brussels"
            },
            "server_type": null,
            "server_reference": null,
            "built_by_users": [
                "John", "Jane"
            ],
            "items": {
                "data": [
                    {
                        "id": 19,
                        "display_name": "Case",
                        "description": "with stand-offs in correct spot",
                        "category": "Components",
                        "option": {
                            "data": {
                                "type": "checkbox",
                                "default_settings": {
                                    "checked": false
                                }
                            }
                        },
                        "value": true
                    },
                    {
                        "id": 24,
                        "display_name": "HDD(s)",
                        "description": "Check if installed.",
                        "category": "Components",
                        "option": {
                            "data": {
                                "type": "checkbox",
                                "default_settings": {
                                    "checked": false
                                }
                            }
                        },
                        "value": true
                    },
                    {
                        "id": 22,
                        "display_name": "Heatsink",
                        "description": "Check if properly attached.",
                        "category": "Components",
                        "option": {
                            "data": {
                                "type": "checkbox",
                                "default_settings": {
                                    "checked": false
                                }
                            }
                        },
                        "value": true
                    },
                    ...
                ]
            }
        }
    ]
}
```

This endpoint retrieves a specific Asset endpoint.

### HTTP Request

`GET https://s3s.eu/api/v2/assets/<ASSET>/<?ID>`

### URL Parameters

Parameter | Description | Required
--------- | ----------- | -----------
ASSET | The asset you wish to access | Yes
ID | The Server reference number for an appliance to retrieve. This is either the asset ID or a BTO specific serial number. | No
page | If no ID is provided, you can use the `page` parameter to browse through different pages. | No
page_size | If no ID is provided, you can use the `page_size` parameter to change the amount of resources per page.<br>`Default: 15`<br>`Max: 50` | No

<aside class="notice">
  If no <code>ID</code> is provided, you will get a list of all available resources in the given asset scope.
</aside>