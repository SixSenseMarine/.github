# [![Github Repo](https://github.com/6SenseSystems/.github/blob/main/.img/LOGO_24.png)](https://github.com/6SenseSystems)  **6-Sense Systems**


Contents
- [  **6-Sense Systems**](#--6-sense-systems)
  - [Device Library Re-factor Checklist](#device-library-re-factor-checklist)
  - [Library Commit Checklist](#library-commit-checklist)
  - [License](#license)
  - [References](#references)

## Device Library Re-factor Checklist

  1. Add `SixSense` namespace around all classes, structs and enums.
  2. Add `static String toString(your_enum_t enumVal)` extension functions to all `enum` objects but place them in the `ext` namespace.
  3. Add `DeviceConfiguration` class for the `Device`.
  4. `Device` class declarations must include:
     1. `device_state_t begin()` function.
     2. `DeviceConfiguration * configuration()` getter.

## Library Commit Checklist

  1. `README.md` updated:
     1. Description.
     2. No dead links.
     3. License terms consistent.
     4. Usage tested and updated.
  2. `CHANGELOG.md` updated:
     1. New version 
     2. Version heading include a title, e.g. "Stable release".
  3. `library.json` updated:
     1. Version number.
     2. Dependencies.
     3. No license.

## License

*GM Consolidated Holdings Pty Ltd* retains ownership of the contents of this repository and the copyright, and other intellectual property rights of whatever nature, including any modifications made to the repository contents.

All 6-Sense Systems repositories are Copyright 2024, *GM Consolidated Holdings Pty Ltd*, ALL RIGHTS RESERVED, and subject to the [license terms](https://github.com/6SenseSystems/.github/blob/main/profile/LICENSE.md) unless expressly noted otherwise.
 

## References
* [PioTemplate repo on github](https://github.com/6SenseSystems/PioTemplate)
* [Calendar Versioning](https://calver.org/)

