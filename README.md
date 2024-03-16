# idp-mame-deb

This repository hosts the necessary files for building the Debian package of the Iskra Delta Partner MAME emulator.

## Building the .deb Package from Prepared Files

To build the package, use the following command:

~~~bash
dpkg-deb --build idp-mame
~~~

## Manually Compiling and Running the Iskra Delta Partner MAME Emulator

1. Clone the MAME Repository

Start by cloning the MAME repository with the following command:

~~~bash
git clone https://github.com/mamedev/mame.git --recurse
~~~

2. Compile the Source Code

Next, compile the source code. This process might take some time, so feel free to grab a coffee in the meantime:

~~~bash
make SUBTARGET=id SOURCES=src/mame/sfrj/idpartner.cpp -j4 REGENIE=1 TOOLS=1
~~~

 > Once compilation is complete, you'll find an executable named `id` in the MAME directory. To avoid conflicts with the pre-existing Linux `id` command, it's advisable to rename this executable to `idp-mame`.

3. Download and Prepare ROMs

To obtain ROMs, you'll need a torrent client. [Download all ROMs from this link](https://pleasuredome.github.io/pleasuredome/mame/index.html), choosing the latest version and the merged option.

After downloading, unzip the merged ROMs zip file into the `roms` directory inside the cloned `mame` directory, without unzipping the individual ROM zips contained within it.

4. Unpack the merged ROMS zip file, but don't unzip individual rom zips inside into the roms directory. 

5. Add Iskra Delta Partner ROM Files

Incorporate the Iskra Delta Partner ROM files [from this repository](usr/share/idp-mame/roms) into your roms directory. Note that some ROM files may be replaced in the process.

6. Prepare the Drive Image

If you have a hdd.img image, use the following command in your MAME directory to prepare the drive image:
~~~bash
./chdman createhd -i hdd.img -o hdd.chd -chs 306,4,32 -ss 256 -f -c none
~~~

7. Run the Emulator

To start the emulator with a hard disk:

~~~bash
./id partnerwfg -window -debug -hard1 ./hdd.chd
~~~

Or, to run it with a floppy disk:

~~~bash
./id partner1f -window -debug -flop1 ./fdd.img
~~~
 

## Useful links

[Creating DEB packages](https://www.iodigital.com/en/history/intracto/creating-debianubuntu-deb-packages)

[Using the serial port in MAME](https://tlindner.macmess.org/?page_id=659)