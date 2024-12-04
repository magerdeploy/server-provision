# Mager Provisioning Script

This repository contains the provisioning scripts for the Mager Deploy.

## Specification

Provisioning utilize PHP Script to provision the system. Script must return anonymous function that return `Generator` instance. To execute unix command use `yield` keyword.

```php
declare(strict_types=1);

return function(): \Generator {
    yield "Upgrading Packages" => <<<CMD
        DEBIAN_FRONTEND=noninteractive sudo apt-get update -y && sudo apt-get upgrade -y
        sudo apt-get install ca-certificates curl wget git jq openssl
    CMD;
};
```

You can also get return value from `yield` keyword.

```php
declare(strict_types=1);

return function(): \Generator {
    $hostname = trim(yield 'hostname');
};
```