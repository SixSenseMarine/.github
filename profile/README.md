# [![Github Repo](https://github.com/6SenseSystems/.github/blob/main/.img/LOGO_24.png)](https://github.com/6SenseSystems)  **6-Sense Systems**


Contents
- [  **6-Sense Systems**](#--6-sense-systems)
  - [Device Library Checklist](#device-library-checklist)
  - [Pre-release Checklist](#pre-release-checklist)
  - [License](#license)
  - [References](#references)

## Device Library Checklist

  1. `platformio.ini` has [https://github.com/6SenseSystems/Device.git](https://github.com/6SenseSystems/Device.git) in the `lib_deps` section.
  2. Run a `Full clean` to rebuild the `/pio/libdeps/` folders.
  2. Do not add `#include <Arduino.h>` to your header files.  It is included by the `Device.h` header file.
  3. Add `SixSense` namespace around all classes, structs and enums.
  4. Add `static String toString(your_enum_t enumVal)` extension functions to all `enum` objects but place them in the `ext` namespace.
  5. Add `DeviceConfiguration` class for the `Device`.
  6. `Device` class declarations must include:
     1. `device_state_t begin()` function.
     2. `DeviceConfiguration * configuration()` getter.

## Pre-release Checklist

  1. Do all decleration (.h) files have `header guards` consistent with the file name. Format to use is `MY_FILE_NAME_H_`?
  2. Do all files have a metadata block at the top with `@file`, `@mainpage`, `intro_sec_Introduction`, `author` and `license` populated?
  3. Have all debug flags been commented out?
  4. Check all public / protected methods and functions:  
     1. have been fully documented with `doxygen` tags.
     2. Have `virtual` in front of the definition.
  5. Ensure all classes have a virtual destructor and that the implementation deletes any FreeRTOS tasks that were created.
  6. `README.md` updated:
     1. Description.
     2. No dead links.
     3. License terms consistent.
     4. Usage tested and updated.
  7. `CHANGELOG.md` updated:
     1. New version 
     2. Version heading include a title, e.g. "Stable release".
  8. `library.json` updated:
     1. `version` number updated, consistent with `CHANGELOG.md`.
     2. `description` is still correct.
     3. `keywords` are still correct.
     4. `repository` git link is correct and works.
     5. `dependencies` have been updated, consistent with `platformio.ini`.
     6. No license.
  9.  Examples placed in the `/lib/YourLibrary/examples/` folder as `ino` files.
  10. Tests placed in the `/tests/` folder.

## License

*GM Consolidated Holdings Pty Ltd* retains ownership of the contents of this repository and the copyright, and other intellectual property rights of whatever nature, including any modifications made to the repository contents.

All 6-Sense Systems repositories are Copyright 2024, *GM Consolidated Holdings Pty Ltd*, ALL RIGHTS RESERVED, and subject to the [license terms](https://github.com/6SenseSystems/.github/blob/main/profile/LICENSE.md) unless expressly noted otherwise.
 

## References
* [PioTemplate repo on github](https://github.com/6SenseSystems/PioTemplate)
* [Calendar Versioning](https://calver.org/)

