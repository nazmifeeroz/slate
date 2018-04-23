---
title: Loyalty Pass API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - php

toc_footers:
  - <a href='http://www.alpome.com'>A Product of Alpome Pte Ltd</a>
  # - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

# includes:
#   - errors

search: true
---

# Introduction

Welcome to the Loyalty Pass API! You can use our API to access SkiesPass API endpoints, which can store and create individual Loyalty Pass in our database. The pass can then be updated with its own endpoints.

This API code will be used in JSON format.

# Authentication

> To authorize:

```php
<?php
use GuzzleHttp\Client;

$client = new Client;

$client->request('POST', 'https://skiespass.com/api/loyalty', [
    'headers'       => [
        'Authorization' => <api_key>,
    ]
]);
?>
```

> Make sure to replace `<api_key>` with your API key.

SkiesPass uses API keys to allow access to the API. Please contact our Web Team to retrieve an API key.

SkiesPass expects for the API key to be included in all API requests to the server in a header that looks like the following:

`POST https://skiespass.com/api/loyalty`

`Authorization: <api_key>`

<aside class="notice">
 Make sure to replace <code><api_key></code> with your API key.
</aside>

# Loyalty Pass

## Creating a pass

> The request should have a body like this:

```php
<?php
$client->request('POST', 'https://skiespass.com/api/loyalty/', [
  'json'    => [
    "template_id"         => "1",
    "name"                => "Guest Name",
    "company_name"        => "Company Co.",
    "membership_level"    => "VIP",
    "membership_number"   => "DODER23W1",
    "points_accumulated"  => "30",
    "points_balance"      => "1250"
  ]
]);
?>
```

> The above command returns JSON structured like this:

```json
{
  "template_id": "1",
  "name": "Guest Name",
  "company_name": "Company Co.",
  "membership_level": "VIP",
  "membership_number": "DODER23W1",
  "points_accumulated": "30",
  "points_balance": "1250"
}
```

> Errors if pass creation is not succesful.

```json
{
  "success": false,
  "error": "API key is not authorized."
}

{
  "success": false,
  "error": "Template ID is invalid."
}

{
  "success": false,
  "error": "Duplicate pass detected."
}
```

In the HTTP request body, a json is expected when creating a pass.

### HTTP Request

`POST https://skiespass.com/api/loyalty/`

### JSON Body Parameters

Parameter | Description
--------- | -----------
template_id | This will be the ID of the template for the pass. It can be found in the template dashboard.
name | Name of member.
company_name | Merchant's company name.
membership_level | This will reflect the membership level of the member from the CRM.
membership_number | Member's number.
points_accumulated | Points that are accumulated from the recent transaction.
points_balanced | Member's points balance.

<aside class="warning">
<strong>WARNING</strong> — the <code>template_id</code> must belong to the <code><api_key></code> provided in the header.
</aside>

## Download Pass

> If pass is created successfully, a json response with a `pass_url` will be returned.

```json
{
  "success": true,
  "pass_url": "https://skiespass.com/loyalty/hgefjbefolgq3284gjbers83"
}
```

Once the pass details are sent and successfully saved in the database, a `url` will be returned where the pass can be downloaded.

### Json Response Parameters

Parameter | Description
--------- | -----------
Success | `true/false` specifies if the pass were successfully created.
error | Describes the error.
pass_url | the `url` to download the pass.

## Updating a pass

> To update a pass:

```php
<?php
$client->request('PUT', 'https://skiespass.com/api/loyalty/update', [
  'json'    => [
    "membership_number"   => "DODER23W1",
    "points_accumulated"  => "30",
    "points_balance"      => "1250"
  ]
]);
?>
```

> If pass is updated successfully.

```json
{
  "success": true,
}
```

This endpoint updates the pass.

### HTTP Request

`PUT https://skiespass.com/api/loyalty/update`

### HTTP Headers

`Authorization: <api_key>`

### JSON Body Parameters

Parameter | Description
--------- | -----------
membership_number | this will validate with the `<api_key>` to match the pass stored


