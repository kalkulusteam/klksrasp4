# KLKS-Raspberry-Pi4-Libs-and-Deps
## All dependencies and libraries to compile KLKS QT wallet on Raspberry Pi4

This is the complete workaround for compiling Kalkulus wallet. 
Alternatively, you can download:
- QT Wallet [Pre-compiled]
https://github.com/kalkulusteam/klks/releases/download/v2.8.0/klks-2.8.0_raspberry_pi4.tar.gz

- Full .img file ready for burn in your SD card:
http://kalkul.us/vault/kalkulus_rasp_system.zip


Otherwise you can proceed manually with those commands:

```
sudo apt-get update && sudo apt-get upgrade 
```
After this command, the Raspi will ask for reboot. Proceed rebooting your Raspi.

```
sudo apt-get install -y pkg-config
sudo apt-get install -y software-properties-common python-software-properties
```

```
wget https://raw.githubusercontent.com/kalkulusteam/klksrasp4/master/script/add-apt-repository.sh
sudo mv add-apt-repository.sh /usr/bin/add-apt-repository
sudo chmod +x /usr/bin/add-apt-repository
sudo add-apt-repository -y ppa:bitcoin/bitcoin
```

```
sudo apt-get -y install build-essential autoconf automake libtool libboost-all-dev libboost-program-options-dev libssl1.0-dev
sudo apt-get -y install libleveldb-dev libgmp-dev libgmp3-dev libcurl4-openssl-dev libcrypto++-dev libqrencode-dev
sudo apt-get -y libminiupnpc-dev autogen libtool libevent-dev libprotobuf-dev protobuf-compiler
sudo apt-get -y install curl g++ git git-core faketime bsdmainutils mingw-w64 g++-mingw-w64 nsis zip ca-certificates python
sudo apt-get -y install libgmp-dev libssl-dev libcurl4-openssl-dev
sudo apt-get -y install qtbase5-dev libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libzmq3-dev
```

```
wget http://download.oracle.com/berkeley-db/db-4.8.30.NC.tar.gz
tar -xzvf db-4.8.30.NC.tar.gz
cd db-4.8.30.NC/build_unix
../dist/configure --enable-cxx
sudo make -j2
sudo make install
```

```
export BDB_INCLUDE_PATH="/usr/local/BerkeleyDB.4.8/include"
export BDB_LIB_PATH="/usr/local/BerkeleyDB.4.8/lib"
sudo ln -s /usr/local/BerkeleyDB.4.8/lib/libdb-4.8.so /usr/lib/libdb-4.8.so
sudo ln -s /usr/local/BerkeleyDB.4.8/lib/libdb_cxx-4.8.so /usr/lib/libdb_cxx-4.8.so
cd
```
Reboot again your Raspi
```
git clone https://github.com/kalkulusteam/klks
cd klks
sudo chmod +x share/genbuild.sh
sudo chmod +x autogen.sh
sudo chmod 755 src/leveldb/build_detect_platform
```
```
./autogen.sh
sudo ./configure --with-gui=qt5 --with-libressl --disable-sse2 CPPFLAGS="-I/usr/local/BerkeleyDB.4.8/include -O2" LDFLAGS="-L/usr/local/BerkeleyDB.4.8/lib"
sudo make -j4
```
