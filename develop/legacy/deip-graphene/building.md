---
description: >-
  Here you will find detailed build instructions, including compile-time
  options, and specific commands for Linux (Ubuntu LTS) or macOS X.
---

# Building

### Compile-time options \(cmake\)

* `CMAKE_BUILD_TYPE=[Release/Debug]` - Specifies whether to build with or without optimization and without or with the symbol table for debugging; unless you are specifically debugging or running tests, we recommend building as release
* `LOW_MEMORY_NODE=[OFF/ON]` - Builds deipd to be a consensus-only low memory node; data and fields not needed for consensus are not stored in the object database; this option is recommended for witnesses and seed-nodes
* `CLEAR_VOTES=[ON/OFF]` - Clears old votes from memory that are no longer required for consensus
* `BUILD_DEIP_TESTNET=[OFF/ON]` - Builds deipd for use in a private testnet; also required for building unit tests
* `SKIP_BY_TX_ID=[OFF/ON]` - By default this is off; enabling will prevent the account history plugin querying transactions by id, but saving around 65% of CPU time when reindexing; enabling this option is a huge gain if you do not need this functionality

### Building under Docker

We ship a Dockerfile. This builds both common node type binaries.

```text
git clone https://gitlab.deip.com/blockchain/node.git
cd deip
docker build -t deip/deip .
```

### Building on Ubuntu 16.04

For Ubuntu 16.04 users, after installing the right packages with `apt` Deip will build out of the box without further effort:

```text
# Required packages
sudo apt-get install -y \
    autoconf \
    automake \
    cmake \
    g++ \
    git \
    libssl-dev \
    libtool \
    make \
    pkg-config \
    python3 \
    python3-jinja2

# Boost packages (also required)
sudo apt-get install -y \
    libboost-chrono-dev \
    libboost-context-dev \
    libboost-coroutine-dev \
    libboost-date-time-dev \
    libboost-filesystem-dev \
    libboost-iostreams-dev \
    libboost-locale-dev \
    libboost-program-options-dev \
    libboost-serialization-dev \
    libboost-signals-dev \
    libboost-system-dev \
    libboost-test-dev \
    libboost-thread-dev

# Optional packages (not required, but will make a nicer experience)
sudo apt-get install -y \
    doxygen \
    libncurses5-dev \
    libreadline-dev \
    perl

git clone https://gitlab.deip.com/blockchain/node.git
cd deip
git submodule update --init --recursive
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Release ..
make -j$(nproc) deipd
make -j$(nproc) cli_wallet
# optional
make install  # defaults to /usr/local
```

### Building on Ubuntu 14.04

\(It is strongly advised to use Ubuntu 16.04 LTS instead.\)

Here are the required packages:

```text
# Required packages
sudo apt-get install -y \
    autoconf \
    cmake3 \
    g++ \
    git \
    libssl-dev \
    libtool \
    make \
    pkg-config \
    doxygen \
    libncurses5-dev \
    libreadline-dev \
    libbz2-dev \
    python-dev \
    perl \
    python3 \
    python3-jinja2
```

The Boost provided in the Ubuntu 14.04 package manager \(Boost 1.55\) is too old. Deip requires Boost 1.58 \(as in Ubuntu 16.04\) and works with versions up to 1.60 \(including\). So building Deip on Ubuntu 14.04 requires downloading and installing a more recent version of Boost.

According to [this mailing list post](http://boost.2283326.n4.nabble.com/1-58-1-bugfix-release-necessary-td4674686.html), Boost 1.58 is not compatible with gcc 4.8 \(the default C++ compiler for Ubuntu 14.04\) when compiling in C++11 mode \(which Deip does\). So we will use Boost 1.60.

Here is how to build and install Boost 1.60 into your user's home directory \(make sure you install all the packages above first\):

```text
export BOOST_ROOT=$HOME/opt/boost_1_60_0
URL='http://sourceforge.net/projects/boost/files/boost/1.60.0/boost_1_60_0.tar.bz2/download'
wget -c "$URL" -O boost_1_60_0.tar.bz2
[ $( sha256sum boost_1_60_0.tar.bz2 | cut -d ' ' -f 1 ) == \
    "686affff989ac2488f79a97b9479efb9f2abae035b5ed4d8226de6857933fd3b" ] \
    || ( echo 'Corrupt download' ; exit 1 )
tar xjf boost_1_60_0.tar.bz2
cd boost_1_60_0
./bootstrap.sh "--prefix=$BOOST_ROOT"
./b2 install
```

Then the instructions are the same as for deip:

```text
git clone https://gitlab.deip.com/blockchain/node.git
cd deip
git submodule update --init --recursive
mkdir build && cd build
cmake -DCMAKE_BUILD_TYPE=Release ..
make -j$(nproc) deipd
make -j$(nproc) cli_wallet
```

### Building on macOS X

Install Xcode and its command line tools by following the instructions here: [https://guide.macports.org/\#installing.xcode](https://guide.macports.org/#installing.xcode). In OS X 10.11 \(El Capitan\) and newer, you will be prompted to install developer tools when running a developer command in the terminal.

Accept the Xcode license if you have not already:

```text
sudo xcodebuild -license accept
```

Install Homebrew by following the instructions here: [http://brew.sh/](http://brew.sh/)

#### Initialize Homebrew:

brew doctor brew update

#### Install deip dependencies:

```text
brew install \
    autoconf \
    automake \
    cmake \
    git \
    boost160 \
    libtool \
    openssl \
    python3 \
    python3-jinja2
```

{% hint style="info" %}
Brew recently updated to boost 1.61.0, which is not yet supported by deip. Until then, this will allow you to install boost 1.60.0.
{% endhint %}

_Optional._ To use TCMalloc in LevelDB:

```text
brew install google-perftools
```

_Optional._ To use cli\_wallet and override macOS's default readline installation:

```text
brew install --force readline
brew link --force readline
```

#### Clone the repository

```text
git clone https://gitlab.com/DEIP/deip-blockchain.git
cd deip
```

#### Compile

```text
export OPENSSL_ROOT_DIR=$(brew --prefix)/Cellar/openssl/1.0.2l/
export BOOST_ROOT=$(brew --prefix)/Cellar/boost@1.60/1.60.0/
git submodule update --init --recursive
mkdir build 
cd build
cmake -DBOOST_ROOT="$BOOST_ROOT" -DCMAKE_BUILD_TYPE=Release ..
make -j$(sysctl -n hw.logicalcpu)
```

Also, some useful build targets for `make` are:

```text
deipd
chain_test
cli_wallet
```

e.g.

```text
make -j$(sysctl -n hw.logicalcpu) deipd
```

This will only build `deipd`.

### To build with TESTNET

```text
export OPENSSL_ROOT_DIR=$(brew --prefix)/Cellar/openssl/1.0.2l/
export BOOST_ROOT=$(brew --prefix)/Cellar/boost@1.60/1.60.0/
git submodule update --init --recursive
mkdir build 
cd build
cmake -DBOOST_ROOT="$BOOST_ROOT" -DCMAKE_BUILD_TYPE=Debug -DBUILD_DEIP_TESTNET=ON ..
make -j$(sysctl -n hw.logicalcpu) chain_test
```

### Building on other platforms

Building instructions for Windows will be soon.

{% hint style="info" %}
The developers normally compile with gcc and clang. These compilers should be well-supported. Community members occasionally attempt to compile the code with mingw, Intel and Microsoft compilers. These compilers may work, but the developers do not use them. Pull requests fixing warnings/errors from these compilers are accepted.
{% endhint %}

