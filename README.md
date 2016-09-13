# DroneLink

## Description

Messaging library for PX4 using mavlink.

## License

BSD 3-clause, see [LICENSE.md](LICENSE.md).

## Authors

See [AUTHORS.md](AUTHORS.md).

## Usage

### gtest

Ubuntu:
[Ubuntu instructions](https://www.eriksmistad.no/getting-started-with-google-test-on-ubuntu/)

Mac:

```
cd wherever
git clone git@github.com:google/googletest.git
cd googletest/
mkdir build
cd build
cmake ..
make -j4
cd ..
sudo cp -r googletest/include/gtest /usr/local/include
sudo cp googlemock/gtest/libgtest.a /usr/local/lib
sudo cp googlemock/gtest/libgtest_main.a /usr/local/lib
```

### Building

```
git submodule update --init --recursive
mkdir build
cd build
```

For releasing:
```
cmake -DCMAKE_BUILD_TYPE=Release ..
```

For debugging:
```
cmake -DCMAKE_BUILD_TYPE=Debug ..
```

```
make
```

### Build with external directory for plugins/integration_tests

The external directory needs to contain the folders `integration_tests` and `plugins`,
and should be organized like the `external_example`.

```
external_example
├── integration_tests
│   ├── CMakeLists.txt
│   └── hello_world_main.cpp
└── plugins
    └── example
        ├── CMakeLists.txt
        ├── example.cpp
        ├── example.h
        ├── example_impl.cpp
        └── example_impl.h
```

To include the external folder in the build, add the folder name to the cmake command
(the path is relative to the root repository path):

```
cmake -DCMAKE_BUILD_TYPE=Debug -DEXTERNAL_DIR:STRING=external_example ..
```

```
make
```

To run the external hello world integration test, do:
```
./external_example/integration_tests/hello_world
```

### Building for iOS

```
cmake -DCMAKE_TOOLCHAIN_FILE=../CrossCompile-iOS.cmake -DCMAKE_BUILD_TYPE=Release ..
```

### Unit-tests

To run tests without output:
```
make test
```

And with output:
```
make check
```

### Integration-tests

Start PX4 e.g. in SITL using `make posix gazebo` and run the integration tests using the commands
below:

```
make simple_connect
integration_tests/simple_connect
```

```
make simple_telemetry
integration_tests/simple_telemetry
```

```
make simple_hover
integration_tests/simple_hover
```