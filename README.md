# doxygen
Contains installation, setup and usage guide for doxygen for code documentation

## Installation
[Reference link](https://doxygen.nl/download.html)

You will require necessary build tools -> g++, python, cmake, flex, bison. For most of them you could go with apt-get install unless you require some specific versions.

- Install them with this command:
```
sudo apt-get install g++ python cmake flex bison build-essential
```

- Validate installation of each dependency one by one:
```
g++ --version
python --version
cmake --version
flex --version
bison --version
```

- Clone official git repo for doxygen:
```
git clone https://github.com/doxygen/doxygen.git
```

- Build and make:
```
mkdir build
cd build
cmake -G "Unix Makefiles" ..
make

- Install build binaries:
```
make install
```
