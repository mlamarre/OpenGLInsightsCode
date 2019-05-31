# Build instructions

## Windows

* Install CMake, 3.10 or later.
* Assuming Visual Studio 2017 x64 below
* Assuming command line in this folder (Chapter 28)

```
mkdir build
cd build
cmake .. -G "Visual Studio 15 2017 Win64"
cmake --build . --target INSTALL --config Release
```

# Running examples
```
cd bin
app_scenario1.exe
```
Press ESC to quit.
Repeat for other executables.
