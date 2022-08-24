### Descriptions
This package allows you to validate an email before actually sending mail to that email.
Checking MX records occurs, including with the help of google.

### Getting started

#### Requirements
- PHP 8.1.5+
- Composer 2+

#### Installation
```
composer require ashvedov/email-validator
```

#### Usage
Anywhere in your code, just include the class EmailValidator in the use section and you're good to go.
It is possible to receive the result of the check as JSON, array or string.

#### Example
```php
use Src\EmailValidator;

$validator = new EmailValidator(
    emails: [
        'simple@example.com',
        'very.common@example.com',
        'abc@example.co.uk',
        'disposable.style.email.with+symbol@example.com',
        'other.email-with-hyphen@example.com',
        'fully-qualified-domain@example.com',
        'user.name+tag+sorting@example.com',
        'example-indeed@strange-example.com',
        23,
        'help@otus.ru'
    ]
);
var_dump($validator->validate()->toArray());
```
##### Result
  - array: 
```
array(3) {
  [23]=>
  array(4) {
    [0]=>
    string(17) "filter_var_errors"
    [1]=>
    string(12) "regex_errors"
    [2]=>
    string(16) "mx_record_errors"
    [3]=>
    string(22) "world_mx_record_errors"
  }
  ["abc@example.co.uk"]=>
  array(2) {
    [0]=>
    string(16) "mx_record_errors"
    [1]=>
    string(22) "world_mx_record_errors"
  }
  ["example-indeed@strange-example.com"]=>
  array(2) {
    [0]=>
    string(16) "mx_record_errors"
    [1]=>
    string(22) "world_mx_record_errors"
  }
}
```
  - JSON: ```{"23":["filter_var_errors","regex_errors","mx_record_errors","world_mx_record_errors"],"abc@example.co.uk":["mx_record_errors","world_mx_record_errors"],"example-indeed@strange-example.com":["mx_record_errors","world_mx_record_errors"]}```
  - String: ```email [23] not valid, email [abc@example.co.uk] not valid, email [example-indeed@strange-example.com] not valid```