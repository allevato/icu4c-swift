# Low-level ICU C APIs for Swift

> :warning: tl;dr: This package contains low-level C APIs. You probably want
> [icu-swift](https://github.com/allevato/icu-swift) instead.

This package defines a module named `ICU4C` that exposes the C API of the
[ICU](http://site.icu-project.org) library to Swift.

The APIs are exposed without renaming (that is, they do not contain the
library version number as a suffix); see the ICU documentation on
[architectural design](http://userguide.icu-project.org/design) for more
information about this.

This package exposes only the raw C API; because of Swift's stricter type
conversions compared to C, it's fairly verbose to use (see the example
below). If you're reading this, you probably want the companion
[icu-swift](https://github.com/allevato/icu-swift) package instead, which
imports `ICU4C` but wraps it in a much more convenient Swift API to use ICU
functionality.

## Usage

If you _really_ want to use the bare C API:

1. Add this package as a dependency in your `Package.swift` file.

    ```swift
    let package = Package(
      ...,
      dependencies: [
        .Package(url: "https://github.com/allevato/icu4c-swift.git", majorVersion: 1, minor: 0),
      ]
      ...,
    )
    ```

1. Import `ICU4C` and call the C functions.

    ```swift
    import ICU4C

    let x: UnicodeScalar = "x"
    let category = u_getIntPropertyValue(Int32(bitPattern: x.value),
                                         UCHAR_GENERAL_CATEGORY)
    print(UInt32(bitPattern: category) == U_LOWERCASE_LETTER.rawValue)  // "true"
    ```
