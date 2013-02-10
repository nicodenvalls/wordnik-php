# PHP client for Wordnik.com API

## Overview

This is a PHP client for the Wordnik.com v4 API. For more information, see http://developer.wordnik.com/ . This client has been generated using the Swagger code generator, which builds robust API clients and beautiful API documentation automatically. If you'd like to learn more about Swagger, visit http://swagger.wordnik.com/ (but you don't need to know anything about Swagger to simply use this API client for Wordnik, this page will tell get you up to speed on that account).

If you need help after reading the below, please find us on Google Groups at https://groups.google.com/group/wordnik-api , @wordnikapi on Twitter, or on #wordnik on IRC.

## Basic Setup

Place the `wordnik` folder that you downloaded somewhere where it can be accessed by your scripts. Create a connection as follows:

```php
<?php
require('./wordnik/Swagger.php');
$myAPIKey = 'YOUR KEY GOES HERE';
$client = new APIClient($myAPIKey, 'http://api.wordnik.com/v4');
?>
```

You'll want to edit those first two lines to reflect the full or relative path to the `wordnik` folder you downloaded (if it isn't in the same directory as your script), and to use your own personal API key. If you don't have an API key yet, you can get one here: http://developer.wordnik.com/ .

## Calling a Method

Once you have a client set up, you need to instantiate an API object for whichever category or categories of items you are interested in working with. For example, to work with the `word` API and apply the method `getTopExample` method, you can do the following:

```php
<?php
$wordApi = new WordApi($client);
$example = $wordApi->getTopExample('irony');
print $example->text;
?>
```

To find out what arguments the method expects, consult the online, interactive documentation at http://developer.wordnik.com/docs , and also check out the method definitions in `wordnik/WordApi.php`.

You can find out what fields to expect in the return value by using the interactive docs. You can also check out the tests in the `tests/` folder in this repository; each method is shown and tested there. In this case, the documentation in `WordAPI.php` shows that `getTopExample` returns an instance of `Example`, so you would examine that class in `wordnik/model/Example.php`.

Some methods, like `getDefinitions`, also take optional keyword parameters which should be specified by name. Again, these are shown in the online documentation and in the method defintions.

```php
<?php
$definitions = $wordAPI->getDefinitions('badger', $partOfSpeech='verb', $sourceDictionaries='wiktionary', $limit=1);
?>
```

The variable `$definitions` is now an array of instances of the `Definition` class defined in `wordnik/models/Definition.php`, as indicated in the documentation for `getDefinition`.


## Testing

The included tests require PHPUnit. If you require PHPUnit to be installed, first get PEAR:

```sh
wget http://pear.php.net/go-pear.phar
php -d detect_unicode=0 go-pear.phar
```

Then install PHPUnit:

```sh
pear config-set auto_discover
pear install pear.phpunit.de/PHPUnit
```

The tests require you to set three environment varibales:

```sh
export API_KEY=your api key
export USER_NAME=some wordnik.com username
export PASSWORD=the user's password
```

The tests can be run as follows:

```sh
phpunit tests/AccountApiTest.php
phpunit tests/WordApiTest.php
phpunit tests/WordsApiTest.php
phpunit tests/WordListApiTest.php
phpunit tests/WordListsApiTest.php
```
