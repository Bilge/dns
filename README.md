# dns

[![Build Status](https://img.shields.io/github/workflow/status/amphp/dns/Continuous%20Integration?style=flat-square)](https://github.com/amphp/dns/actions)
[![License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](./LICENSE)

`amphp/dns` provides asynchronous DNS resolution for PHP based on [Amp](https://github.com/amphp/amp).

## Installation

```bash
composer require amphp/dns
```

## Example

```php
<?php

require __DIR__ . '/examples/_bootstrap.php';

$githubIpv4 = Amp\Dns\resolve("github.com", Dns\Record::A);
pretty_print_records("github.com", $githubIpv4);

$googleIpv4 = Amp\Dns\resolve("google.com", Dns\Record::A);
$googleIpv6 = Amp\Dns\resolve("google.com", Dns\Record::AAAA);

$firstGoogleResult = Amp\Promise\first([$googleIpv4, $googleIpv6]);
pretty_print_records("google.com", $firstGoogleResult);

$combinedGoogleResult = Amp\Dns\resolve("google.com");
pretty_print_records("google.com", $combinedGoogleResult);

$googleMx = yield Amp\Dns\query("google.com", Amp\Dns\Record::MX);
pretty_print_records("google.com", $googleMx);
```
