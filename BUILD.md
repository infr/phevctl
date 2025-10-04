# Build Instructions

## Requirements

Unix based OS

- Tested on Debian and variants including Ubuntu, WSL & Raspberry Pi.
- Also tested on MacOS (Catalina).

### Raspberry Pi

Use the steps below (updated 4.10.2025)

```
⏺ # Install dependencies
  sudo apt-get install build-essential cmake git

  # Build and install msg-core
  git clone https://github.com/papawattu/msg-core
  cd msg-core
  mkdir build
  cd build
  cmake ..
  make
  sudo make install
  cd ~

  # Build and install cJSON
  git clone https://github.com/DaveGamble/cJSON.git
  cd cJSON
  mkdir build
  cd build
  cmake ..
  make
  sudo make install
  cd ~

  # Build and install phevcore (with fixes)
  git clone https://github.com/phev-remote/phevcore.git
  cd phevcore
  sed -i '3s/^/# /' CMakeLists.txt
  sed -i '/add_splint/,+2 s/^/# /' CMakeLists.txt
  mkdir build
  cd build
  cmake ..
  make
  sudo make install
  sudo ldconfig
  cd ~

  # Build phevctl (with fixes)
  git clone https://github.com/phev-remote/phevctl.git
  cd phevctl
  sed -i 's/find_library(ARGP_LIB argp)/find_library(ARGP_LIB argp)\nif(NOT ARGP_LIB)\n  set(ARGP_LIB "")\nendif()/' CMakeLists.txt
  mkdir build
  cd build
  cmake ..
  make

  # Run it
  ./phevctl --help
```


### Debian based and Mac OS

Use the steps below, or have a look at [this repository](https://github.com/steady286/phevbuild).

```
sudo apt-get install build-essential cmake git
git clone https://github.com/papawattu/msg-core
cd msg-core
mkdir build
cd build
cmake ..
make
sudo make install

cd ../../
git clone https://github.com/phev-remote/phevcore.git
cd phevcore
mkdir build
cd build
cmake ..
make
sudo make install
cd ../../

git clone https://github.com/DaveGamble/cJSON.git
cd cJSON
mkdir build
cd build
cmake ..
make
sudo make install
cd ../../

git clone https://github.com/phev-remote/phevctl.git
cd phevctl
mkdir build
cd build
cmake ..
make

./phevctl --help
```
