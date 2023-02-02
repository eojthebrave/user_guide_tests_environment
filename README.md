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

## Working with User Guide files in the container

This environment also contains the tooling required to run the various build scripts for the User Guide content. In the [User Guide](https://www.drupal.og/project/user_guide) project these scripts are found in the _scripts/_ directory. And are used the build the output of the guide that's shown on Drupal.org, as well as the PDF and e-book versions.

You can mount the User Guide files into the container using a _.ddev/docker-compose.local.yaml_ file like so:

```yaml
version: '3.6'

services:
  web:
    volumes:
      - /Users/joe/Sites/user_guide:/user_guide
```

You might need to manually install the "URW Palladio L" font if LaTex complains about it.

```
cd /usr/share/fonts/truetype
sudo curl -I https://www.fontsplace.com/free/fonts/u/urw_palladio_l_roman.ttf
```

Then you should be able to run the build scripts like so:

```
cd /user_guide/scripts
./mkall.sh 10.0.x en
```
