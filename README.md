xctool_wrapper
==============

XCTool is great at wrapping up `xcodebuild`'s persnickety input and unmanageable output. It has the added benefit of adding the `build-tests` and `run-tests` subcommands, which allow you to save time by reusing the compilation products for multiple test runs.

To help you leverage these features in `Rakefile`s, the `xctool_wrapper` gem adds an idiomatic Ruby wrapper around XCTool using the builder pattern.

## Basic Usage

```
require 'xctool'
xctool = XCTool::Builder.new("my-workspace", "my-scheme") # instantiate an xctool builder
xctool.with_test_sdk("iphonesimulator7.0").clean.test # configure xctool
puts xctool # outputs: `xctool -reporter 'pretty' -workspace 'my-workspace' -scheme 'my-scheme' -sdk 'iphonesimulator7.0' -configuration 'Release' clean test -test-sdk 'iphonesimulator7.0' -freshSimulator -parallelize -failOnEmptyTestBundles -simulator iphone`
sh xctool.as_cmd # you are responsible for shelling out to invoke xctool, located on PATH.
```

## Contributing

You should add test coverage and run tests before committing.

### Setup

`bundle`

### Running the tests

`./ci.sh` or `bundle && rake`.

## TODO

* Support all xctool options (e.g. arch is not supported)
* Dynamically support available SDKs
* Tightly couple with xctool versions and invoke xctool
