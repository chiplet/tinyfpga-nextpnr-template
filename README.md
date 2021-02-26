# Description
This repository is a minimal starting point for using the TinyFPGA-BX development board with yosys and nextpnr.

# Setup

## Install prerequisites
Installing qt5 is only required if you want to use nextpnr in graphical mode.

### Ubuntu
```shell
sudo apt-get install build-essential clang bison flex libreadline-dev \
                     gawk tcl-dev libffi-dev git mercurial graphviz   \
                     xdot pkg-config python python3 libftdi-dev qt5-default
```

### macOS
Install dependencies with [homebrew](https://brew.sh/)

```shell
brew install cmake python boost eigen qt5
```

Installing qt5 is only required if you want to install the GUI environment for nextpnr. You also need to add the location qt5 binaries to your `PATH` environment variable with one of the following commands depending on which shell you are using, and restart your shell for the changes to take effect.

**bash**
```shell
echo 'export PATH="/usr/local/opt/qt/bin:$PATH"' >> ~/.bash_profile
```
**zsh**
```shell 
echo 'export PATH="/usr/local/opt/qt/bin:$PATH"' >> ~/.zshrc
```

## Install [icestorm](http://www.clifford.at/icestorm/)
On macOS, remove the `-j$(nproc)` flags from the `make` commands, or use the `-jN` flag, where `N` should be replaced the number of cores you have in your machine.

```shell
mkdir icestorm-build
cd icestorm-build

git clone https://github.com/cliffordwolf/icestorm.git icestorm
cd icestorm
make -j$(nproc)
sudo make install
cd ..


git clone https://github.com/cseed/arachne-pnr.git arachne-pnr
cd arachne-pnr
make -j$(nproc)
sudo make install
cd ..

git clone https://github.com/cliffordwolf/yosys.git yosys
cd yosys
make -j$(nproc)
sudo make install
cd ..

pip install --user tinyprog
```

## Install [nextpnr]()
On macOS, remove the `-j$(nproc)` flags from the `make` commands, or use the `-jN` flag, where `N` should be replaced the number of cores you have in your machine.

```shell
git clone https://github.com/YosysHQ/nextpnr nextpnr
cd nextpnr
cmake . -DARCH=ice40 -DBUILD_GUI=ON
make -j$(nproc)
sudo make install
```
## Install tinyprog
```shell
pip3 install tinyprog
```

# Build
Build the project:
```shell
make
```

Program the TinyFPGA B-series board with the bitstream:
```shell
make prog
```


