# WordPress Scanner Action

> Performs syntax checks, virus scanning and plugins and themes vulnerability checks for WordPress sites

[![Support Level](https://img.shields.io/badge/support-active-green.svg)](#support-level) [![Release Version](https://img.shields.io/github/release/10up/wp-scanner-action.svg)](https://github.com/10up/wp-scanner-action/releases/latest) [![MIT License](https://img.shields.io/badge/License-MIT-yellow.svg)](https://github.com/10up/wp-scanner-action/blob/trunk/LICENSE.md) [![Automated Tests](https://github.com/10up/wp-scanner-action/actions/workflows/tests.yml/badge.svg)](https://github.com/10up/wp-scanner-action/actions/workflows/tests.yml)

This Github Action performs standard scanning for WordPress sites which includes PHP syntax checks, virus scanning and plugins and themes vulnerabilities scanning.

# API Access

This Action leverages our own [WP-CLI Vulnerability Scanner](https://github.com/10up/wpcli-vulnerability-scanner) to perform the known vulnerabilities scanning of WordPress plugins and themes. WP-CLI Vulnerability Scanner works with [WPScan](https://wpscan.com), [Patchstack](https://patchstack.com/) and [Wordfence Intelligence](https://www.wordfence.com/threat-intel/) to check reported vulnerabilities; you can choose any one of these three to use.
***Note**: Authentication is optional for the Wordfence Intelligence Vulnerability API.*

# Inputs

| Name | Required | Default | Description |
| --- | --- | --- | --- |
| `vuln_api_provider` | False | `wordfence` | The vulnerability API provider for the WordPress plugins and themes scanning. Supported values: `wordfence`, `patchstack` and `wpscan` |
| `vuln_api_token` | False | - | The API token to authenticate against the vulnerability API provider. This input is optional if `vuln_api_provider` is set to `wordfence` |
| `disable_vuln_scan` | False | `false` | Disable the WordPress plugins and themes vulnerability scanner |
| `virus_scan_update` | False | `true` | Update the ClamAV definitions database before executing the virus scanner (recommended) |
| `disable_virus_scan` | False | `false` | Disable the ClamAV virus scanner |
| `phpsyntax_enable_debug` | False | `false` | The PHP syntax checks could generate a large output depending on the amount of PHP files in the repository, for this reason the output is suppresed by default. Set this input to `true` if you want to visualize the full output. Useful for troubleshooting in case the PHP syntax checks fails |
| `disable_phpsyntax_check` | False | `false` | Disable the PHP syntax checks |
| `content_dir` | False | `$GITHUB_WORKSPACE` | Location of the `wp-content` directory inside the repository. Set this input to `./` if you have a `wp-content` based repository |
| `wp_core_version` | False | `latest` | WordPress core version to use for the plugins and themes vulnerability scanner. Must match the version of your WordPress site for better results |
| `composer_build` | False | `false` | Install the Composer dependencies in your `composer.json` file before executing the WordPress plugins and themes vulnerability scanner. The `composer.json` file must exists in the repository's root directory. Set this input to `true` if you install plugins and themes via Composer in CI. ***Note: This won't affect your final deploy artifact*** |
| `no_fail` | False | `false` | Exits the scanner without failing even if any issues are found |


# Examples

## Basic example with Composer dependencies

This example assumes that you have a `wp-content` based repository and uses [Patchstack](https://patchstack.com/) as the API provider.

```yaml
name: "PHP Syntax Check, virus scanning, and WP Plugins & Themes vulnerability scanning"

on:
  push:
    branches:
      - '**'

jobs:
  wp-scanner:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4
        with:
          ref: ${{ github.ref }}
      
      - name: WordPress Scanner
        uses: 10up/wp-scanner-action@v1
        with:
          vuln_api_provider: 'patchstack'
          vuln_api_token: ${{ secrets.PATCHSTACK_TOKEN }}
          content_dir: './'
          wp_core_version: '6.5.5'
          composer_build: 'true'
```

## Plugins and Themes under version control

This example assumes that you have all plugins and themes under version control inside a directory named `wp-content` in the repository.

```yaml
name: "PHP Syntax Check, virus scanning, and WP Plugins & Themes vulnerability scanning"

on:
  push:
    branches:
      - '**'

jobs:
  wp-scanner:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4
        with:
          ref: ${{ github.ref }}
      
      - name: WordPress Scanner
        uses: 10up/wp-scanner-action@v1
        with:
          vuln_api_provider: 'patchstack'
          vuln_api_token: ${{ secrets.PATCHSTACK_TOKEN }}
          content_dir: './wp-content'
          wp_core_version: '6.5.5'
```

# Support Level

**Active:** 10up is actively working on this, and we expect to continue work for the foreseeable. Bug reports, feature requests, questions, and pull requests are welcome.

# Changelog

A complete listing of all notable changes to this Github Action are documented in [CHANGELOG.md](https://github.com/10up/wp-scanner-action/blob/trunk/CHANGELOG.md).

# Contributing

Please read [CODE_OF_CONDUCT.md](https://github.com/10up/wp-scanner-action/blob/trunk/CODE_OF_CONDUCT.md) for details on our code of conduct, [CONTRIBUTING.md](https://github.com/10up/wp-scanner-action/blob/trunk/CONTRIBUTING.md) for details on the process for submitting pull requests to us, and [CREDITS.md](https://github.com/10up/wp-scanner-action/blob/trunk/CREDITS.md) for a listing of maintainers and contributors.

# Like what you see?

<p align="center">
<a href="http://10up.com/contact/"><img src="https://10up.com/uploads/2016/10/10up-Github-Banner.png" width="850"></a>
</p>