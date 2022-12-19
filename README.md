# Drupal User Guide Tests

This project consists of the configuration necessary to set up a DDEV-Local (Docker) environment for executing the tests in the https://www.drupal.org/project/user_guide_tests code. These tests validate the steps in the [Drupal User Guide](https://www.drupal.org/project/user_guide). As well as generate screenshots in various languages for the guide.

## Usage

- [Install DDEV-Local](https://ddev.readthedocs.io/en/latest/)
- Clone this repository
- Execute `ddev start` from the root directory
- Followed by `ddev composer install`

## Running the tests

```shell
ddev exec ./vendor/bin/phpunit --verbose -c web/core/ web/modules/contrib/user_guide_tests/tests/src/FunctionalJavascript/
```

While the tests are running you can visit https://user-guide-tests.ddev.site:7900 (password: secret) to watch them run in Chrome.

## Details

In addition to a standard Drupal 9 + DDEV-Local setup this project provides an additional Docker container with Chrome & Firefox installed and configuration for executing Drupal's functional test suite. The user_guide_tests project consists of a number of tests that step through the same process as outlined in the Drupal User Guide tutorials and generates language specific screenshots in the process.

## Updating composer dependencies of user_guide_tests module

Edit the root composer.json from this repo with something like:

```json
        "0": {
            "type": "path",
            "url": "/var/www/html/web/modules/contrib/user_guide_tests"
        },
```

More info https://www.drupal.org/docs/develop/using-composer/tricks-for-using-composer-when-developing-a-contrib-module-locally
