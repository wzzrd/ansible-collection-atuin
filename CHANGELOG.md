# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.1.3]

#### Fixed

- Made collection check mode compatible

## [2.1.1]

#### Fixed

- Small linting errors

## [2.1.0]

#### Added

- Support for atuin 18.3.0 (which changed the artifact naming convention)

## [2.0.2]

#### Added

- Added .gitleads.toml to repo to prevent security scanners from barfing over fake
  PostgreSQL password

#### Added

## [2.0.1]

#### Added

- Add some documentation on the atuin_client_users variable

## [2.0.0]

#### Added

- Iterate over list of users and build a configuration file for them
- Drop podman molecule scenario in favor of docker for now

#### Changed

- Change default listen address from default_ipv4 to 127.0.0.1

## [1.0.1]

- First version uploaded to Ansible Galaxy

## [1.0.0]

### Changed

- Initial release
