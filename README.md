# Freshdesk PHP SDK API v2 

[![Latest Stable Version](http://poser.pugx.org/songxunzhao/freshdesk-php-sdk/v)](https://packagist.org/packages/songxunzhao/freshdesk-php-sdk) [![Total Downloads](http://poser.pugx.org/songxunzhao/freshdesk-php-sdk/downloads)](https://packagist.org/packages/songxunzhao/freshdesk-php-sdk) [![Latest Unstable Version](http://poser.pugx.org/songxunzhao/freshdesk-php-sdk/v/unstable)](https://packagist.org/packages/songxunzhao/freshdesk-php-sdk) [![License](http://poser.pugx.org/songxunzhao/freshdesk-php-sdk/license)](https://packagist.org/packages/songxunzhao/freshdesk-php-sdk) [![PHP Version Require](http://poser.pugx.org/songxunzhao/freshdesk-php-sdk/require/php)](https://packagist.org/packages/songxunzhao/freshdesk-php-sdk)

This is a PHP 5.5+ SDK for the [Freshdesk](https://www.freshdesk.com) API v2.

If you have questions, please contact me or open an issue on GitHub.

## Quick Start
```phpg
require __DIR__ . '/vendor/autoload.php';
use \Freshdesk\Api;

$api = new Api("your_freshdesk_api_key", "your_freshdesk_domain");

$all = $api->tickets->all();
$some = $api->tickets->all(['page' => 2]);
$new = $api->tickets->create($data);
$updated = $api->tickets->update($data);
$api->tickets->delete($id);
$existing = $api->tickets->view($id);

//Responses are simple arrays, e.g.:
$id = $existing['id'];
$first = $all[0];

```

## Framework Integration

- Symfony - [FreshdeskBundle](https://github.com/mpclarkson/freshdesk-bundle) 
- Laravel/Lumen - [Freshdesk Larvel Service Provider](https://github.com/mpclarkson/freshdesk-laravel) .

## Installation

To integrate this library into your application, use [Composer](https://getcomposer.org).

Add `mpclarkson/freshdesk-php-sdk` to your **composer.json** file:

```json
{
    "require": {
        "songxunzhao/freshdesk-php-sdk": "dev-master"
    }
}
```

Then run:

```bash
php composer.phar install
```

## API Overview

Full documentation is available [here](docs/ApiIndex.md)

### Getting started

Creating a new API instance is very easy. All you need is your Freshdesk 
API key and your Freshdesk domain.

```php
require __DIR__ . '/vendor/autoload.php';
use \Freshdesk\Api;

$api = new Api("your_freshdesk_api_key", "your_freshdesk_domain");
```

### Resources

The available methods for each resource are available via a public
property on the api, for example:

```php
//Contacts
$contacts = $api->contacts->update($contactId, $data);

//Agents
$me = $api->agents->current();

//Companies
$company = $api->companies->create($data);

//Groups
$deleted = $api->groups->delete($groupId);

//Tickets
$ticket = $api->tickets->view($filters);

//Time Entries
$time = $api->timeEntries->all($ticket['id']);

//Conversations
$ticket = $api->conversations->note($ticketId, $data);

//Categories
$newCategory = $api->categories->create($data);

//Forums
$forum = $api->forums->create($categoryId, $data);

//Topics
$topics = $api->topics->monitor($topicId, $userId);

//Comments
$comment = $api->comments->create($forumId);

//Email Configs
$configs = $api->emailConfigs->all();

//Products
$product = $api->products->view($productId);

//Business Hours
$hours = $api->businessHours->all();

//SLA Policy
$policies = $api->slaPolicies->all();

```

### Responses

All responses are arrays of data. Please refer to Freshdesk's documentation
for further information. 

### Filtering

All `GET` requests accept an optional `array $query` parameter to filter
results. For example:

```php
//Page 2 with 50 results per page
$page2 = $this->forums->all(['page' => 2, 'per_page' => 50]);

//Tickets for a specific customer
$tickets = $this->tickets->view(['company_id' => $companyId]);

```

Please read the Freshdesk documentation for further information on
filtering `GET` requests.

## Contributing

This is a work in progress and PRs are welcome. Please read the 
[contributing guide](.github/CONTRIBUTING.md).

Nearly all api calls are available except for the `Solutions` and `Surveys`, 
which Freshdesk has not yet implemented.

- [ ] Solutions
- [ ] Surveys
- [ ] Uploading files is not yet supported
- [ ] More tests. You can never have enough!
- [ ] Nicer documentation

## Author

The library was written and maintained by [Zhao SongXun](https://songxunzhao.github.io/) 
from [Hilenium](https://hilenium.com).

## Reference

* [Freshdesk API Documentation](https://developer.freshdesk.com/api/)
