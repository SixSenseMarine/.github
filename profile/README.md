# [![Github Repo](https://github.com/6SenseSystems/.github/blob/main/.img/LOGO_24.png)](https://github.com/6SenseSystems)  **6-Sense Systems**


Contents
- [  **6-Sense Systems**](#--6-sense-systems)
  - [Developer Guidelines](#developer-guidelines)
    - [Style Guide](#style-guide)
    - [Pull-request Checklist](#pull-request-checklist)
    - [Device Library Checklist](#device-library-checklist)
  - [Code Example](#code-example)
  - [License](#license)
  - [References](#references)

## Developer Guidelines

The [6-Sense Systems](https://github.com/6SenseSystems) repositories are not open-source but subject to the [license terms](https://github.com/6SenseSystems/.github/blob/main/profile/LICENSE.md) unless expressly noted otherwise. *Please secure the IP that you download and do not share it unless permission has been obtained.*

All these repositories form part of commercial products and development of the codebase must contribute towards the commercial objectives and the feature roadmap of the [6-Sense Systems](https://github.com/6SenseSystems) product manager(s). Pull requests will only be considered if they are on the approved product backlog. *Before forking any repository and starting work on it, approval must be obtained from the administrator for the new features or changes.*

Contributors to the [6-Sense Systems](https://github.com/6SenseSystems) codebase should follow these guidelines to ensure that the codebase remains consistent. Please use the checklists below before commening work as they will be applied during review of all pull requests.

### Style Guide

The style guidelines below should be implemented. An example of code that conforms to these guidelines is shown [below](#code-example).

**Namespaces**

All classes, structs, enums and global/static functions must be wrapped in the `SixSense` namespace. Extension functions must be added to the `ext` namespace.

**Naming Conventions**

The following naming conventions are used:
* Use [`PascalCase`](https://www.freecodecamp.org/news/programming-naming-conventions-explained/) for all class and struct names.
* Use [`camelCase`](https://www.freecodecamp.org/news/programming-naming-conventions-explained/) for all public scope functions and variables.
* Use underscore-prefixed [`_camelCase`](https://www.freecodecamp.org/news/programming-naming-conventions-explained/) for all private and protected scope functions and variables.
* Use [`snake_case_t`](https://www.freecodecamp.org/news/programming-naming-conventions-explained/) for type definitions, including the `_t` at the end. 
* Use `SCREAMING_SNAKE_CASE` for preprocessor directives/defines, enum values and enum titles.

**Code Documentation**

* Code must be fully documented in [doxygen](https://www.doxygen.nl/) compatible style to allow generation of API documentation.
* Versioning follows the [Calendar Versioning](https://calver.org/). The `CHANGELOG.md` must be maintained and shorthand dot points on code changes must be added for every version. Contributors may not use release version numbers (e.g. `1.0.1`, or `1.0.1+12`) but should use the pre-release post script, e.g. `1.0.1-3`.
* Version numbers must always be updated in the `library.json` file.

### Pull-request Checklist

  1. Do all decleration (.h) files have `header guards` consistent with the file name. Format to use is `MY_FILE_NAME_H_`?
  2. Do all files have a metadata block at the top with `@file`, `@mainpage`, `intro_sec_Introduction`, `author` and `license` populated?
  3. Have all debug flags been commented out?
  4. Check all public / protected methods and functions:  
     1. have been fully documented with [doxygen](https://www.doxygen.nl/) tags; and
     2. have `virtual` in front of the definition.
  5. Ensure all classes have a virtual destructor and that the implementation deletes any `FreeRTOS` tasks that were created.
  6. Ensure the `README.md` has been updated:
     1. is the `Description` still valid?
     2. Check for dead links.
     3. Check the `License` terms are correct and consistent.
     4. Make sure the `Usage` is tested and updated.
  7. `CHANGELOG.md` updated:
     1. Add a new [version](https://calver.org/). 
     2. Add a version a title, e.g. "Pre-release, breaking changes".
  8. Make sure the `library.json` is updated:
     1. Update the `version` number consistent with `CHANGELOG.md`.
     2. Ensure `description` is still correct.
     3. Ensure `keywords` are still correct.
     4. Ensure `repository` git link is correct and works.
     5. `dependencies` have been updated, consistent with `platformio.ini`.
     6. Ensure there is no `license` section.
  9.  Update examples in the `/lib/YourLibrary/examples/` folder as `ino` files.
  10. Update tests placed in the `/tests/` folder.

### Device Library Checklist

All libraries that provide an interface with another device and/or peripheral should implement the `SixSense::Device` and `SixSense::DeviceConfiguration` interfaces. See the [example below](#code-example).

  1. Ensure that `platformio.ini` has [https://github.com/6SenseSystems/Device.git](https://github.com/6SenseSystems/Device.git) in the `lib_deps` section.
  2. Run a `Full clean` to rebuild the `/pio/libdeps/` folders.
  2. Do not add `#include <Arduino.h>` to your header files.  It is included by the `Device.h` header file.
  3. Add `SixSense` namespace around all classes, structs and enums.
  4. Add `static String toString(your_enum_t enumVal)` extension functions to all `enum` objects but place them in the `ext` namespace.
  5. Add `DeviceConfiguration` class for the `Device`.
  6. `Device` class declarations must include:
     1. `device_state_t begin()` function.
     2. `DeviceConfiguration * configuration()` getter.


## Code Example


A sample class declaration is shown below:

```C++
/*!
 * @file MyClass.h
 *
 * @mainpage Example implementation class.
 *
 * @section intro_sec_Introduction
 *
 * This simple implementation class defines a configuration class with
 * one property and a device implementation that demonstrates how to use 
 * the configuration class during initialization.
 * 
 * @section author Author
 *
 * Gerhard Malan for GM Consolidated Holdings Pty Ltd.
 *
 * @section license License
 * 
 * Copyright 2024, GM Consolidated Holdings Pty Ltd, ALL RIGHTS 
 * RESERVED. License terms available at:
 * 
 * https://github.com/6SenseSystems/.github/blob/main/profile/LICENSE.md)
 * 
 */

/// header Guards
#ifndef MY_CLASS_H_
#define MY_CLASS_H_

/// implement the @ref Device interface
#include <Device.h>

/// All objects must exist in the @ref SixSense namespace, except extension 
/// methods.
namespace SixSense{

/// @brief Inherit from Device and implement the pure virtual 
/// methods.
class MyClass: public Device {

private: 

    /// @brief Pointer to the device configuration properties.
    MyConfig * _config;

public:

    /// @brief Default constructor.
    MyClass(): _config(new MyConfig()){}

    /// @brief Default destructor.
    ~MyClass(){}

    /// @brief Returns a pointer to the device configuration properties.
    /// @return a pointer to the device configuration properties.
    MyConfig * configuration(){
        return _config;
    }

    /// @brief Initializes the MyClass instance.
    /// @return The DeviceState at the end of the initialization.
    device_state_t begin(){

        // request the configuration values from the device 
        // (not implemented in this example).
        configuration()->requestConfiguration();

        // check if the configuration values have been returned 
        if (ready()){
            // set the device state to ready
            setState(STATE_READY);  
        } else {
            // set the device state to STATE_ERR
            setState(STATE_ERR);
        }
        // return the device state
        return getState();
    };

};

} // end SixSense namespace
#endif 

```


## License

*GM Consolidated Holdings Pty Ltd* retains ownership of the contents of this repository and the copyright, and other intellectual property rights of whatever nature, including any modifications made to the repository contents.

All 6-Sense Systems repositories are Copyright 2024, *GM Consolidated Holdings Pty Ltd*, ALL RIGHTS RESERVED, and subject to the [license terms](https://github.com/6SenseSystems/.github/blob/main/profile/LICENSE.md) unless expressly noted otherwise.
 

## References
* [PioTemplate repo on github](https://github.com/6SenseSystems/PioTemplate)
* [Calendar Versioning](https://calver.org/)
* [<span style="text-decoration: underline">Doxy,gen</span>](https://www.doxygen.nl/)
* [Programming Naming Conventions – Camel, Snake, Kebab, and Pascal Case Explained](https://www.freecodecamp.org/news/programming-naming-conventions-explained/)

