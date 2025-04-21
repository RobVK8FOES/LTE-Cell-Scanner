This is a fork of LTE-Cell-Scanner with CellSearch patched to work with BladeRF 2.0 hardware. This is ideal for finding cells to decode with LTESniffer because you can use your BladeRF 2.0 to search for AND decode an LTE cell, without having to unplug your cellular antenna between your BladeRF and HackRF/RTL-SDR. LTE-Tracker doesn't work, I don't really care about that function anyway. Tested and working on DragonOS FocalX R35.

## Build
```
cd
git clone https://github.com/RobVK8FOES/LTE-Cell-Scanner.git
cd LTE-Cell-Scanner
mkdir build
cd build
cmake ../ -DUSE_BLADERF=1
make -j`nproc`
```

## Usage
- CellSearch
```
~/LTE-Cell-Scanner/build/src/CellSearch -s 763000000
```
Above tries to search for an LTE Cell at 763MHz. 

Example output:
```
Detected a FDD cell! At freqeuncy 763MHz, try 0
    cell ID: 45
     PSS ID: 0
    RX power level: -11.4183 dB
    residual frequency offset: 114.466 Hz
                     k_factor: 1
try peak 0 tdd_flag 1
Detected the following cells:
DPX:TDD/FDD; A: #antenna ports C: CP type ; P: PHICH duration ; PR: PHICH resource type
DPX CID A      fc   freq-offset RXPWR C nRB P  PR CrystalCorrectionFactor
FDD  45 2    763M          114h -11.4 N  50 N one 1.0000001500208448579
```
Searching a range of frequencies is not recommended with the BladeRF 2.0, as it is extremely slow to scan compared to the HackRF and RTL-SDR (on my machine, anyway...) I recommend using your countries spectrum regulation authorities licence database website to locate LTE cells near your location and targeting the frequency directly using the command above. For example, here in Australia we can utilize the ACMA's 'Site Location Map' to search for all transmitter sites with an Emission Designator of 10M0W7D. The webpage will proceed to overlay all LTE cell sites matching this search on a map.

## Install
```
cd ~/LTE-Cell-Scanner/build/src
sudo make install
```
CAUTION: This will overwrite any previous installation of LTE Cell Scanner. For example, if using DragonOS FocalX, it will overwite the CellSearch pre-installed out-of-the-box) I recommend renaming the CellSearch binary to 'CellSearch-BladeRF' and then manually copying it to /usr/local/bin/

