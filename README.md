# User Friendly Exception

This is a **very simple** PHP library for a reusable `UserFriendlyException` class.

Using `UserFriendlyException` indicates that the `$message` passed is safe to and clear enough to be bubbled up to the end user.



## Prerequisites

You will need:

* An applicationn being written for [PHP](https://www.php.net/) 8.2 (or higher up to 9.0)
* [Composer](https://getcomposer.org/)



## Installation

Using composer, run:

```bash
composer require christianjbrown/user-friendly-exception
```



## Usage

Throwing the exception after catching a non-user-friendly exception.

```php
use RuntimeException;
use ChristianBrown\UserFriendlyException\UserFriendlyException;

try {
	// ...
  // Technical issue here
  // ...
} catch (RuntimeException $e) {
  throw new UserFriendlyException('We encountered a technical issue. Please try again later', 0, $e);
}
```

Later passing the contents of `UserFriendlyException` directly to the end users

```php
use ChristianBrown\UserFriendlyException\UserFriendlyExceptionInterface;
use Throwable;

$app = new Application();
try {
  $responseText = $app->run();
  $response = new Response($responseText, 200);
} catch (UserFriendlyExceptionInterface $e) {
  $response = new Response($e->getMessage(), $e->getCode() ?: 500);
} catch (Throwable $e) {
  $response = new Response('An unknown error occured, try again later', 500);
}

return $response;
```



## Dependencies

This library has no dependencies.


During development, this library uses:

* [christianjbrown/phpcs-wrapper](https://github.com/christianjbrown/phpcs-wrapper) for checking code style via `composer check-style`
* [christianjbrown/php-cs-fixer-wrapper](https://github.com/christianjbrown/php-cs-fixer-wrapper) for code style cleanup via `composer fix-style`
* [phpunit/phpunit](https://github.com/sebastianbergmann/phpunit) for unit testing via `composer test`



## Contributing

Before creating a pull request, ensure that you have

1. Fixed your code style with `composer fix-style`, and checked style with `composer check-style`.
2. Checked test coverage with `composer test`. 100% line, branch, function and method coverage is required. 100% path coverage is encouraged.



## License

Copyright © 2023 Christian Brown

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.