# Changelog

All notable changes to the ProGlove SDK will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- New features go here

### Changed
- Changes to existing functionality go here

### Fixed
- Bug fixes go here

---

# Release 2.0.0.0

---

## [2.0.0.0] — 2026-10-28

_Components:_ sdk: 2.0.0.0,driver: 2.0.0.0,wrist-sdk: 2.0.0.0,wrist-driver: 2.0.0.0,

### Added

- Each glove status message carries the time the glove captured it, in host time, with an error bound. Readers that decode only the message are not affected

### Changed

- Versions follow the hardware generation: the Gen 2 glove SDK and driver, and the wrist camera SDK and driver, start at 2.0.0. The API does not change from 0.4.14.1

### Fixed

- macOS: the wrist camera driver stops a camera cleanly while a frame is in flight

---

