## Setup of the Serial Console, WSL and VIM Text Editor : PreLab
### Install Advanced Serial Console for Windows : PuTTY
	- Download from : https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html
	- Choose 64-bit x86 link to download and follow the installation steps
	
### For Windows Subsystem for Linux:
-How to uninstall WSL(if any) entirely : 

	https://pureinfotech.com/uninstall-wsl-windows-11/
-Install WSL through Windows powershell:

	> wsl --install
-In Windows Powershell (as admin):

   	dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
-Restart your machine to complete the WSL install and update to WSL 2
  	> download and run kernel package from here
	
   	https://learn.microsoft.com/en-us/windows/wsl/install-manual#step-3---enable-virtual-machine-feature
 -Set WSL2 as the default version: 
 
 	wsl --set-default-version 2
-Install Linux distribution form here:

	https://apps.microsoft.com/store/detail/ubuntu-2004/9N6SVWS3RX71?hl=en-us&gl=us
-Check the version: 

	wsl -l -v
-Set WSL2 as the default version: 

	wsl --set-default-version 2		
-Upgrade the WSL version for Ubuntu:

	wsl --set-version Ubuntu 2
-If you want to set Ubuntu as default, use:
	
	wsl -s Ubuntu-20.04
-To use the Ubuntu simply use:

	ubuntu
	(OR) You may even start the program from start menu
-Refer this link for any other information: https://learn.microsoft.com/en-us/windows/wsl/install (or) 

P2.2 : TERMINAL : Try out the WSL and create text file

	- mkdir Suraj
	- cd Suraj
	- nano trial.txt
	- cat trial.txt
- This will print the trial input given in the text file

P2.3 : TEXT EDITOR-VIM : 
Install GVim on Ubuntu

	- sudo apt-get update
	- sudo apt install vim-gtk3
	- gvim


## PICO Setup - Lab 2

### Install wget
	sudo apt install wget
### Script to setup the Pico
	wget https://raw.githubusercontent.com/raspberrypi/pico-setup/master/pico_setup.sh
### Make the setup executable
	chmod +x pico_setup.sh
### Run the script
	./pico_setup.sh
### Get SDK and examples
	cd ~/
	mkdir pico
	cd pico
	git clone -b master https://github.com/raspberrypi/pico-sdk.git
	cd pico-sdk
	git submodule update --init
	cd ..
	git clone -b master https://github.com/raspberrypi/pico-examples.git
### Install the Toolchain
	sudo apt update
	sudo apt install cmake gcc-arm-none-eabi libnewlib-arm-none-eabi build-essential
	sudo apt install libstdc++-arm-none-eabi-newlib
### Update the SDK
	cd pico-sdk
	git pull
	git submodule update
### Building "Hello World"
	cd pico-examples
	mkdir build
	cd build
	export PICO_SDK_PATH=/home/suraj/pico/pico-sdk
	cmake ..
	cd hello_world
	make -j4
-See that "Built target hello_world" is displayed with no errors!

### Load and Run "Hello World"

-Connect RP2040 to the Laptop and hold down the BOOTSEL and RESET buttons to put it in USB Mass Storage Mode

-Copy the file "helloworld.uf2" onto the Mass Storage Device (Observe that RP2040 reboots and unmounts from the laptop)

### Open Putty to see serial output
	- Give the following settings:
		> Connection type: Serial
		> Serial Line should be same as the COM port that RP2040 is using from Device Manager
		> Speed: 115200
		> Save the settings so that they can be loaded the next time you open PuTTY
		> Click Open to see the Advanced Serial Console
(Output contains "Hello World" being printed on the serial console in loop)

## PART 4 : HELLO, BLINKENLIGHT

### Create a new C file

-Neopixel LED should blink each time there is a Serial output

-Use the code from WS2812.c and from hello_world.c for reference and construct helloLED.c

-Copy the "adafruit_qtpy_rp2040.h" header file from /home/suraj/pico/pico-sdk/src/boards/include/boards/

-Paste in the current working directory where the C file is placed

-Make sure the helloLED folder is in /../pico-examples

### Build "helloLED"

	cd pico-examples
	rm -r build && mkdir build && cd build
	export PICO_SDK_PATH=/home/suraj/pico/pico-sdk
	cmake ..
	cd helloLED
	make -j4
	
-See that "Built target helloLED" is displayed with no errors!

### Edit the CMAKE file

-Combine the CMAKE files of ws2812 from /../pico-examples/pio/ws2812/CMakeLists.txt and hellousb from /../pico-examples/hello_world/usb/CMakeLists.txt

-Add two lines in the end to enable USB out and disable UART out

-Save the file and put it in the helloLED folder of the SDK

## Load and Run "helloLED"

-Connect RP2040 to the Laptop and hold down the BOOTSEL and RESET buttons to put it in USB Mass Storage Mode

-Copy the file "helloLED.uf2" onto the Mass Storage Device (Observe that RP2040 reboots and unmounts from the laptop)

### Open Putty to see serial output

	- Give the following settings:
		> Connection type: Serial
		> Serial Line should be same as the COM port that RP2040 is using from Device Manager
		> Speed: 115200
		> Save the settings so that they can be loaded the next time you open PuTTY
		> Click Open to see the Advanced Serial Console

(Output contains "Neopixel Blinks!" being printed on the serial console in loop while the NEOPIXEL LED blinks white on the RP2040)




## (To work with WINDOWS)
### Go to section 9.2 from the Getting started with Raspberry Pi Pico document
#### Install the ARM GNU Tool chain
![image](https://user-images.githubusercontent.com/69215958/195835802-f68db6eb-481a-4aa6-9c2a-d767d084df77.png)
#### Install CMake
![image](https://user-images.githubusercontent.com/69215958/195836898-587a5c1b-9671-4c71-b14f-628fbfe31956.png)
#### Install Build Tools for VS
![image](https://user-images.githubusercontent.com/69215958/195837734-dd893955-9a28-44c0-8474-8089eabe71e6.png)
#### Install Git for Windows
Make sure to select only the C++ Build Tools : Desktop Development for C++
![image](https://user-images.githubusercontent.com/69215958/195839481-35b20450-571d-4d1c-a2f5-a965dd379afe.png)

	
