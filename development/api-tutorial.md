# API Usage Tutorial

## In EspoCRM

1. Go to Admninistration > Roles and create a new role with permissions you want to grand for the API user.
2. Go to Administration > API Users and create a new API User. Select the created role. An **API Key** will be generated, you will need to use it in your API requests further.

## In external application

### PHP

1. Create a new PHP file: `EspoApiClient.php` with the code copied from [here](api-client-php.md#class).
2. Include this file in the place where you want to call EspoCRM API and use it. See the code below.

```php
<?php

require_once('EspoApiClient.php');

$url = 'https://address-of-your-espocrm';
$apiKey = 'copy API key from API user to here';

$client = new EspoApiClient($url);
$client->setApiKey($apiKey);

// example creating a new lead
try {
    $response = $client->request('POST', 'Lead', [
        'firstName' => 'Test',
        'lastName' => 'Hello',
    ]);
} catch (\Exception $e) {
    $errorCode = $e->getCode();
}
```

### Javascript (Nodejs)

1. Create a new JS file: `espocrm-api-client.js` with the code copied from [here](api-client-js.md#module).
2. Use `require` function to include the module in the place where you want to call EspoCRM API and use it. See the code below.

```js
const Client = require('./espocrm-api-client');

const client = new Client(
    'https://address-of-your-espocrm',
    'copy API key from API user to here'
);

// POST request example
var payload = {
    name: 'some name',
    type: 'Customer',
};
client.request('POST', 'Account', payload)
    .then(
        (response) => {
            // success
            console.log(response);
        }
    )
    .catch(
        (res) => {
            // error
            console.log(res.statusCode, res.statusMessage);
        }
    );
```