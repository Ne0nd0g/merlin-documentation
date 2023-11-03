# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)
and this project adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

Use `sphinx-build --version` to determine the current version of sphinx in use

## 2.1.0 - 2023-11-03

### Added

- Added `parrot` & `secure` commands for the Agent CLI arguments and Makefile
  - Added `parrot` command to the Merlin CLI 
- Documentation for proxying Agent DLL provided by @HuskyHacks in [PR 136](https://github.com/Ne0nd0g/merlin/pull/136)

## 2.0.0 - 2023-10-27

### Added 

- Merlin Command Line Interface (CLI) help
  - Added `cli`, `commands`, and `listeners` help pages
- Top level FAQ section

### Changed

- Updated documentation and associated commands to support Merlin version 2.0.0
- Moved the menu commands from the Server section to the CLI section
- Condensed Quick Start into a single page
- Updated the Custom Build section with a Merlin Agent makefile variables
- Moved logging information to individual sections like Server and CLI

## 1.0.0 - 2023-05-15

### Added

- Initial release
- Successfully built with: `sphinx-build 7.0.1`