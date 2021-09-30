# Drupal User Guide Tests

This project consists of the configuration necessary to set up a DDEV-Local (Docker) environment for executing the tests in the https://www.drupal.org/project/user_guide_tests code. These tests validate the steps in the [Drupal User Guide](https://www.drupal.org/project/user_guide). As well as generate screenshots in various languages for the guide.

## Usage

- [Install DDEV-Local](https://ddev.readthedocs.io/en/latest/)
- Clone this repository
- Execute `ddev start` from the root directory
- Followed by `ddev composer install`

## Details

In addition to a standard Drupal 9 + DDEV-Local setup this project provides an additional Docker container with Chromium installed and configuration for executing Drupal's functional test suite. The user_guide_tests project consists of a number of tests that step through the same process as outlined in the Drupal User Guide tutorials and generates language specific screenshots in the process.
