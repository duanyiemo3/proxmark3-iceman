The iceman fork
---------------
##::THIS FORK IS HIGHLY EXPERIMENTAL::

##NOTICE:      

There is so much in this fork,  with all fixes and additions its basically the most enhanced fork to this day for the Proxmark3 device.


##OFFICAL 
The official Proxmark repository is found here: https://github.com/Proxmark/proxmark3

##NEWS: 

## Build Status Travis CI
[![Build Status](https://travis-ci.org/iceman1001/proxmark3.svg?branch=master)](https://travis-ci.org/iceman1001/proxmark3)

## Build Status Coverity Scan
[![Coverity Scan Build Status](https://scan.coverity.com/projects/5117/badge.svg)](https://scan.coverity.com/projects/proxmark3-iceman-fork)


## Coverity Scan Config && Run

Download the Coverity Scan Self-buld and install it.
You will need to configure  ARM-NON-EABI- Compiler for it to use:

:: Configure
cov-configure --comptype gcc --compiler  /opt/devkitpro/devkitARM/bin/arm-none-eabi-gcc

::run it (I'm running on Ubuntu)
cov-build --dir cov-int make all

:: make a tarball
tar czvf proxmark3.tgz cov-int

:: upload it to coverity.com

## Whats changed?

Whats so special with this fork?  I have scraped the web for different enhancements to the PM3 source code and not all of them ever found their way to the master branch. 
Among the stuff is

	* Jonor's hf 14a raw timing patch
	* Piwi's updates. (usually gets into the master)
	* Piwi's "topaz" branch
	* Piwi's "hardnested" branch 
	* Holiman's iclass, (usually gets into the master)
	* Marshmellow's fixes (usually gets into the master)
	* Midnitesnake's Ultralight,  Ultralight-c enhancements
	* Izsh's lf peak modification / iir-filtering
	* Aspers's tips and tricks from inside the PM3-gui-tool, settings.xml and other stuff.
	* My own desfire, Ultralight extras, LF T55xx enhancements, bugs fixes (filelength, hf mf commands ), TNP3xxx lua scripts,  Awid26,  skidata scripts (will come)
	* other obscure patches like for the sammy-mode,  (offline you know), tagidentifications, defaultkeys. 
	* Minor textual changes here and there.
	* Simulation of Ultralight/Ntag.
	* Marshmellow's and my "RevEng" addon for the client.  Ref: http://reveng.sourceforge.net/    Now using reveng1.31
	* Someone's alternative bruteforce Mifare changes.. (you need the two other exe to make it work)

	* A Bruteforce for T55XX passwords against tag.
	* A Bruteforce for AWID 26, starting w a facilitycode then trying all 0xFFFF cardnumbers via simulation. To be used against a AWID Reader.
	* A Bruteforce for HID,  starting w a facilitycode then trying all 0xFFFF cardnumbers via simulation. To be used against a HID Reader.
	* Blaposts Crapto1 v3.3
					  
    * icsom's  legic script and legic enhancements

---	
Straight from the CHANGELOG
---
  - Added `lf guard clone/sim` (iceman)
  - Added `lf pyramd clone/sim` (iceman) 
  - trying to fix "hf 14b" command to be able to read CALYPSO card.	 (iceman)
  - `hf legic load`, it now loads faster and a casting bug is gone. (iceman)
  - Added `hf legic calccrc8` added a method to calculate the legic crc-8 value (iceman)
  - `hf legic decode` fixed the output overflow bugs, better printing (iceman)
  - Coverity Scan fixes a lot of resource leaks, etc (iceman)
  - Added `lf presco *` commands started (iceman) 
  - Added `lf hid wiegand` added a method to calculate WIEGAND in different formats, (iceman)
  - `hf mf chkkeys` better printing, same table output as nested, faster execution and added Adam Lauries "try to read Key B if Key A is found" (iceman)
  - `hf mf nested` better printing and added Adam Lauries "try to read Key B if Key A is found" (iceman)
  - `hf mf mifare` fixing the zero parity path, which doesn't got called. (iceman) 
  - Updated the @blapost's Crapto1 implementation to v3.3 (blapost) 
  - `hf mf c*` updated the calling structure and refactored of the chinese magic commands (iceman, marshmellow)
  - Started to add Peter Fillmore's  EMV fork into Iceman fork. ref: https://github.com/peterfillmore/proxmark3  (peter fillmore,  iceman)
  - Added Travis-CI automatic build integration with GitHub fork. (iceman)
  - Updated the Reveng 1.30 sourcecode to 1.31 from Reveng projecthomepage (iceman)
  
  - Added possibility to write direct to a Legic Prime Tag (MIM256/1024) without using values from the 'BigBuffer' -> 'hf legic writeRaw <addr> <value>' (icsom)
  - Added possibility to decrease DCF values at address 0x05 & 0x06 on a Legic Prime Tag 
		DCF-value will be pulled from the BigBuffer (address 0x05 & 0x06) so you have to 
		load the data into the BigBuffer before with 'hf legic load <path/to/legic.dump>' & then
		write the DCF-Values (both at once) with 'hf legic write 0x05 0x02'  (icsom)
  - Added script `legic.lua` for display and edit Data of Legic-Prime Tags (icsom)
  - Added the experimental HITAG_S support (spenneb)
  - Added topaz detection to `hf search` (iceman)
  - Fixed the silent mode for 14b to be used inside 'hf search' (iceman)
	
---	
	
Give me a hint, and I'll see if I can't merge in the stuff you have. 

I don't actually know how to make small pull-request to github :( and that is the number one reason for me not pushing a lot of things back to the PM3 master.
	
PM3 GUI:
--------
I do tend to rename and move stuff around, the official PM3-GUI from Gaucho will not work so well. *sorry*	


	  
DEVELOPMENT:
------------
This fork now compiles just fine on 
	windows/mingw environment with Qt5.3.1 & GCC 4.8
	Ubuntuu 1404, 1510
	Mac OS X

SETUP AND BUILD FOR UBUNTU
--------------------------

GC made updates to allow this to build easily on Ubuntu 14.04.2 LTS or 15.10
See https://github.com/Proxmark/proxmark3/wiki/Ubuntu%20Linux

Run 
	-> sudo apt-get install p7zip git build-essential libreadline5 libreadline-dev libusb-0.1-4 libusb-dev libqt4-dev perl pkg-config wget

Follow these instructions
Get devkitARM release 41 from SourceForge (choose either the 64/32 bit depending on your architecture, it is assumed you know how to check and recognize your architecture):

(64-bit) http://sourceforge.net/projects/devkitpro/files/devkitARM/previous/devkitARM_r41-x86_64-linux.tar.bz2/download
(32-bit) http://sourceforge.net/projects/devkitpro/files/devkitARM/previous/devkitARM_r41-i686-linux.tar.bz2/download

Extract the contents of the .tar.bz2:
	->  tar jxvf devkitARM_r41-<arch>-linux.tar.bz2

Create a directory for the arm dev kit:
	->  sudo mkdir -p /opt/devkitpro/

Move the ARM developer kit to the newly created directory:
	-> sudo mv devkitARM /opt/devkitpro/

Add the appropriate environment variable:
	-> export PATH=${PATH}:/opt/devkitpro/devkitARM/bin/

Add the environment variable to your profile:
	-> echo 'PATH=${PATH}:/opt/devkitpro/devkitARM/bin/ ' >> ~/.bashrc

Clone iceman fork
	-> git clone https://github.com/iceman1001/proxmark3.git

Get the latest commits	
	-> git pull

CLEAN COMPILE	
	-> make clean && make all
	
Flash the BOOTROM
	-> client/flasher -b /dev/ttyACM0 bootrom/obj/bootrom.elf

Flash the FULLIMAGE	
	-> client/flasher /dev/ttyACM0 armsrc/obj/fullimage.elf
	
Change into the client folder. 	
	-> cd client
	
Run the client	
	-> ./proxmark3 /dev/ttyACM0
						   

January 2015, Sweden
iceman at host iuse.se

BUYING A PROXMARK 3
-------------------

The Proxmark 3 device is available for purchase (assembled and tested) from the following locations:

   * http://www.elechouse.com  (new and revised hardware package 2015)  

   I recommend you to buy this version. 

--------------------------------------------------------------------------

Most of the ultra-low-volume contract assemblers could put
something like this together with a reasonable yield. A run of around
a dozen units is probably cost-effective. The BOM includes (possibly-
outdated) component pricing, and everything is available from Digikey
and the usual distributors.

If you've never assembled a modern circuit board by hand, then this is
not a good place to start. Some of the components (e.g. the crystals)
must not be assembled with a soldering iron, and require hot air.

The schematics are included; the component values given are not
necessarily correct for all situations, but it should be possible to do
nearly anything you would want with appropriate population options.

The printed circuit board artwork is also available, as Gerbers and an
Excellon drill file.


LICENSING:

This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 2 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program; if not, write to the Free Software
Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA


Jonathan Westhues
user jwesthues, at host cq.cx

May 2007, Cambridge MA
