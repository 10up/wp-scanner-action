# Changelog

All notable changes to this project will be documented in this file, per [the Keep a Changelog standard](http://keepachangelog.com/).

## [Unreleased] - TBD

## [v1.0.1] - 2024-10-11

### Updated
- Removed verbosity from `freshclam` DB update command
- Force trailing slash for `WP_CONTENT_DIR` variable
- Ensure `wp-config.php` file is deleted from `wordpress` dir in `setup_wordpress` function
- Separate vuln scanner into 2 functions, themes and plugins
- Separate vuln scanner setup into its own function
- Use `--porcelain` flag in vuln WPCLI command to avoid using `grep`
- Set the `vuln_api_provider` as not required and set its default value to `wordfence`

## [v1.0.0] - 2024-07-22

### Added
- Initial action release

[Unreleased]: https://github.com/10up/wp-scanner-action/compare/trunk...develop
[v1.0.1]: https://github.com/10up/classifai/compare/v1.0.0...v1.0.1
[v1.0.0]: https://github.com/10up/wp-scanner-action/tree/c4aab3b08c0daf7c34c850f86d68981dbed855a7
