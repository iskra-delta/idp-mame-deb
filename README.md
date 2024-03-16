# idp-mame-deb

This repository contains the files required to build the Debian package for the Iskra Delta Partner MAME emulator.

## Building the .deb package from prepared files

`dpkg-deb --build idp-mame`

## Manually Compiling and Running Iskra Delta Partner MAME emulator

1. Clone the MAME repository.

`git clone https://github.com/mamedev/mame.git --recurse'

2. Run make (...and go fetch yourself a coffee)

`make SUBTARGET=id SOURCES=src/mame/sfrj/idpartner.cpp -j4 REGENIE=1 TOOLS=1`

After the compilation finished, the MAME directory will contain `id` executable. Since there already is a program called *id* on
Linux, we recommend you rename this to idp-mame to prevent conflicts.

3. Download ROMS into roms directory under your main mame directory

You will need Torrent client. [Download all roms from here.](https://pleasuredome.github.io/pleasuredome/mame/index.html). Select latest version, merged.

4. Unpack the merged ROMS zip file, but don't unzip individual rom zips inside into the roms directory. 

5. Add the Iskra Delta Parner ROM files [from this repository](usr/share/idp-mame/roms). Some ROM files might be overwritten.

6. Prepare drive image. For example if you have `hdd.img` image available, do this in your mame directory.

`./chdman createhd -i hdd.img -o hdd.chd -chs 306,4,32 -ss 256 -f -c none`

7. Run the emulator.

With hard disk

`./id partnerwfg -window -debug -hard1 ./hdd.chd`

With floppy disk

`./id partner1f -window -debug -flop1 ./fdd.img`
 

## Useful links

[Creating DEB packages](https://www.iodigital.com/en/history/intracto/creating-debianubuntu-deb-packages)

[Using the serial port in MAME](https://tlindner.macmess.org/?page_id=659)
